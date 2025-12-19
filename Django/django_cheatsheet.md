# 🐍 Django Cheat Sheet (4.x/5.x)

> Quick reference for day-to-day Django development (~2000 lines)

## 📑 What's Covered

| # | Section | Key Topics |
|---|---------|------------|
| 0 | **Quick Reference** | One-page condensed commands, Production checklist |
| 1 | **Project/App Setup** | startproject, settings structure, env vars, secrets |
| 2 | **URLs & Views** | FBV vs CBV, path/re_path, namespaces, generic views |
| 3 | **Templates** | Inheritance, filters/tags, context processors, static/media |
| 4 | **Models & ORM** | Fields, relations, queries, select_related, annotations, transactions |
| 5 | **Migrations** | makemigrations/migrate, squashing, data migrations, conflicts |
| 6 | **Admin** | Customization, inlines, list_display, actions, permissions |
| 7 | **Forms** | Forms vs ModelForms, validation, formsets |
| 8 | **Authentication** | Custom user, permissions/groups, login/logout, sessions |
| 9 | **Middleware** | Request/response cycle, CSRF, CORS, custom middleware |
| 10 | **REST APIs (DRF)** | Serializers, viewsets, routers, auth, pagination |
| 11 | **Testing** | TestCase vs pytest-django, factories, mocking, coverage |
| 12 | **Security** | CSRF, XSS, SQL injection, SECURE_* settings, ALLOWED_HOSTS |
| 13 | **Performance** | Caching, query optimization, pagination, async views |
| 14 | **Deployment** | WSGI/ASGI, Gunicorn, Nginx, collectstatic, logging, health checks |
| 15 | **Common Recipes** | Top 15 tasks (slugs, email, soft delete, bulk ops, webhooks, etc.) |
| 16 | **Troubleshooting** | Common errors & fixes (AppRegistryNotReady, DisallowedHost, etc.) |

**Format per section:** What it is → When to use → Minimal example → Gotchas

---

## 📋 One-Page Condensed Reference

```text
PROJECT SETUP
─────────────
django-admin startproject config .    # Create project in current dir
python manage.py startapp appname     # Create new app
pip freeze > requirements.txt         # Save dependencies

ESSENTIAL COMMANDS
──────────────────
python manage.py runserver            # Dev server (port 8000)
python manage.py makemigrations       # Create migrations
python manage.py migrate              # Apply migrations
python manage.py createsuperuser      # Create admin user
python manage.py shell                # Django shell
python manage.py collectstatic        # Collect static files
python manage.py test                 # Run tests
python manage.py check --deploy       # Production security check

QUICK PATTERNS
──────────────
# FBV
def view(request):
    return render(request, 'template.html', {'key': value})

# CBV
class MyView(TemplateView):
    template_name = 'template.html'

# URL
path('route/', view, name='name')
path('item/<int:pk>/', DetailView.as_view(), name='detail')

# Model
class Model(models.Model):
    field = models.CharField(max_length=100)
    class Meta:
        ordering = ['-created']

# Form
class MyForm(forms.ModelForm):
    class Meta:
        model = Model
        fields = ['field1', 'field2']

# Query
Model.objects.filter(field__icontains='x').exclude(active=False)
Model.objects.select_related('fk').prefetch_related('m2m')
Model.objects.annotate(count=Count('related'))

# Auth
@login_required
def protected_view(request): ...

LOGIN_URL = '/accounts/login/'
LOGIN_REDIRECT_URL = '/dashboard/'
```

---

## ✅ Production Readiness Checklist

```text
[ ] DEBUG = False
[ ] SECRET_KEY from environment variable
[ ] ALLOWED_HOSTS configured
[ ] HTTPS enforced (SECURE_SSL_REDIRECT = True)
[ ] CSRF_COOKIE_SECURE = True
[ ] SESSION_COOKIE_SECURE = True
[ ] SECURE_HSTS_SECONDS > 0
[ ] Database credentials in env vars
[ ] Static files collected (collectstatic)
[ ] Media files on cloud storage (S3)
[ ] Logging configured
[ ] Error monitoring (Sentry)
[ ] Database backups scheduled
[ ] Run: python manage.py check --deploy
```

---

# 1. Project & App Setup

## What It Is
Project = container for settings/config. App = reusable module with models/views.

## When to Use
- **startproject**: Once per project
- **startapp**: For each logical feature (users, blog, api)

## Commands
```bash
# Create project (config in current directory)
django-admin startproject config .

# Create app
python manage.py startapp blog

# With custom settings
django-admin startproject mysite --template=https://github.com/user/template.zip
```

## Settings Structure
```python
# config/settings/base.py
from pathlib import Path
import os

BASE_DIR = Path(__file__).resolve().parent.parent.parent

SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY', 'dev-key-change-me')
DEBUG = os.environ.get('DJANGO_DEBUG', 'True') == 'True'
ALLOWED_HOSTS = os.environ.get('DJANGO_ALLOWED_HOSTS', 'localhost').split(',')

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Local apps
    'blog.apps.BlogConfig',
]
```

## Environment Variables
```python
# Using python-dotenv
# .env file
DJANGO_SECRET_KEY=your-secret-key
DATABASE_URL=postgres://user:pass@localhost/db

# settings.py
from dotenv import load_dotenv
load_dotenv()

SECRET_KEY = os.getenv('DJANGO_SECRET_KEY')

# Or use django-environ
import environ
env = environ.Env()
environ.Env.read_env()
SECRET_KEY = env('SECRET_KEY')
```

## 🚨 Gotchas
1. **Never commit `.env`** - Add to `.gitignore`
2. **Forgot to add app to INSTALLED_APPS** - Models won't migrate, templates won't load

---

# 2. URLs & Views

## FBV (Function-Based Views)
```python
# views.py
from django.shortcuts import render, get_object_or_404, redirect
from django.http import JsonResponse, Http404

def post_list(request):
    """When: Simple logic, quick endpoints"""
    posts = Post.objects.filter(published=True)
    return render(request, 'blog/post_list.html', {'posts': posts})

def post_detail(request, slug):
    post = get_object_or_404(Post, slug=slug)
    return render(request, 'blog/post_detail.html', {'post': post})

def api_data(request):
    return JsonResponse({'status': 'ok', 'data': [1, 2, 3]})
```

## CBV (Class-Based Views)
```python
# views.py
from django.views.generic import ListView, DetailView, CreateView, UpdateView, DeleteView
from django.contrib.auth.mixins import LoginRequiredMixin
from django.urls import reverse_lazy

class PostListView(ListView):
    """When: Standard CRUD, DRY code, inheritance needed"""
    model = Post
    template_name = 'blog/post_list.html'
    context_object_name = 'posts'
    paginate_by = 10
    
    def get_queryset(self):
        return Post.objects.filter(published=True)

class PostCreateView(LoginRequiredMixin, CreateView):
    model = Post
    fields = ['title', 'content']
    success_url = reverse_lazy('post_list')
    
    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)
```

## URL Patterns
```python
# urls.py
from django.urls import path, include, re_path

app_name = 'blog'  # Namespace

urlpatterns = [
    # Basic
    path('', views.post_list, name='list'),
    
    # With converters
    path('post/<int:pk>/', views.post_detail, name='detail'),
    path('post/<slug:slug>/', views.post_by_slug, name='by_slug'),
    
    # CBV
    path('posts/', PostListView.as_view(), name='post_list'),
    
    # Include app URLs
    path('api/', include('api.urls', namespace='api')),
    
    # Regex (rare)
    re_path(r'^archive/(?P<year>[0-9]{4})/$', views.archive),
]

# Template usage: {% url 'blog:detail' pk=post.pk %}
# Python usage: reverse('blog:detail', kwargs={'pk': 1})
```

## Path Converters
| Converter | Matches | Example |
|-----------|---------|---------|
| `str` | Non-empty string (excludes `/`) | `<str:name>` |
| `int` | Zero or positive integer | `<int:pk>` |
| `slug` | ASCII letters, numbers, hyphens, underscores | `<slug:slug>` |
| `uuid` | UUID format | `<uuid:id>` |
| `path` | Non-empty string including `/` | `<path:file_path>` |

## 🚨 Gotchas
1. **URL order matters** - More specific patterns first
2. **Forgot `app_name`** - Can't use namespaced URLs like `{% url 'app:view' %}`

---

# 3. Templates

## Template Inheritance
```html
<!-- base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}Site{% endblock %}</title>
    {% block extra_css %}{% endblock %}
</head>
<body>
    {% include '_navbar.html' %}
    
    <main>
        {% block content %}{% endblock %}
    </main>
    
    {% block extra_js %}{% endblock %}
</body>
</html>

<!-- child.html -->
{% extends 'base.html' %}

{% block title %}Page Title{% endblock %}

{% block content %}
<h1>Hello {{ user.username }}</h1>
{% endblock %}
```

## Common Tags & Filters
```html
<!-- Variables -->
{{ variable }}
{{ variable|default:"N/A" }}
{{ name|lower|truncatewords:30 }}
{{ date|date:"Y-m-d" }}
{{ price|floatformat:2 }}
{{ text|linebreaks }}
{{ html_content|safe }}

<!-- Conditionals -->
{% if user.is_authenticated %}
    Welcome, {{ user.username }}
{% elif user.is_anonymous %}
    Please log in
{% else %}
    Something else
{% endif %}

<!-- Loops -->
{% for item in items %}
    {{ forloop.counter }}. {{ item.name }}
{% empty %}
    No items found.
{% endfor %}

<!-- Static files -->
{% load static %}
<link href="{% static 'css/style.css' %}" rel="stylesheet">
<img src="{% static 'images/logo.png' %}" alt="Logo">

<!-- URLs -->
{% url 'blog:detail' pk=post.pk %}
{% url 'blog:list' as post_url %}
```

## Context Processors
```python
# context_processors.py
def site_settings(request):
    """Makes variables available in ALL templates"""
    return {
        'SITE_NAME': 'My Site',
        'CURRENT_YEAR': datetime.now().year,
    }

# settings.py
TEMPLATES = [{
    'OPTIONS': {
        'context_processors': [
            # ... defaults ...
            'myapp.context_processors.site_settings',
        ],
    },
}]
```

## Static & Media Files
```python
# settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
STATIC_ROOT = BASE_DIR / 'staticfiles'  # For collectstatic

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'

# urls.py (dev only)
from django.conf import settings
from django.conf.urls.static import static

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

## 🚨 Gotchas
1. **Forgot `{% load static %}`** - Static tags won't work
2. **Using `{{ var|safe }}` carelessly** - XSS vulnerability risk

---

# 4. Models & ORM

## Field Types
```python
from django.db import models
from django.contrib.auth.models import User

class Post(models.Model):
    # Text
    title = models.CharField(max_length=200)
    slug = models.SlugField(unique=True)
    content = models.TextField()
    excerpt = models.TextField(blank=True)
    
    # Numbers
    view_count = models.IntegerField(default=0)
    rating = models.DecimalField(max_digits=3, decimal_places=2)
    price = models.FloatField(null=True, blank=True)
    
    # Boolean
    is_published = models.BooleanField(default=False)
    
    # DateTime
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    publish_date = models.DateField(null=True)
    
    # Files
    image = models.ImageField(upload_to='posts/%Y/%m/')
    document = models.FileField(upload_to='docs/')
    
    # Relationships
    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name='posts')
    category = models.ForeignKey('Category', on_delete=models.SET_NULL, null=True)
    tags = models.ManyToManyField('Tag', blank=True, related_name='posts')
    
    class Meta:
        ordering = ['-created_at']
        verbose_name_plural = 'Posts'
        indexes = [
            models.Index(fields=['slug']),
            models.Index(fields=['-created_at', 'is_published']),
        ]
        constraints = [
            models.UniqueConstraint(fields=['author', 'slug'], name='unique_author_slug'),
        ]
    
    def __str__(self):
        return self.title
    
    def get_absolute_url(self):
        from django.urls import reverse
        return reverse('blog:detail', kwargs={'slug': self.slug})
```

## Relationships
```python
# One-to-Many (ForeignKey)
author = models.ForeignKey(User, on_delete=models.CASCADE)
# on_delete options: CASCADE, PROTECT, SET_NULL, SET_DEFAULT, DO_NOTHING

# Many-to-Many
tags = models.ManyToManyField('Tag')
# With through model:
members = models.ManyToManyField(User, through='Membership')

# One-to-One
profile = models.OneToOneField(User, on_delete=models.CASCADE)
```

## Query Patterns
```python
# Basic queries
Post.objects.all()
Post.objects.filter(is_published=True)
Post.objects.exclude(author=None)
Post.objects.get(pk=1)  # Raises DoesNotExist if not found
Post.objects.first()
Post.objects.last()
Post.objects.count()
Post.objects.exists()

# Field lookups
Post.objects.filter(title__icontains='django')
Post.objects.filter(created_at__year=2024)
Post.objects.filter(created_at__gte=datetime.now())
Post.objects.filter(author__username='john')
Post.objects.filter(tags__name__in=['python', 'django'])

# Chaining
Post.objects.filter(is_published=True).exclude(author=None).order_by('-created_at')[:10]

# Q objects for OR
from django.db.models import Q
Post.objects.filter(Q(title__icontains='django') | Q(content__icontains='django'))

# Values
Post.objects.values('title', 'author__username')
Post.objects.values_list('id', flat=True)
```

## select_related vs prefetch_related
```python
# select_related: ForeignKey, OneToOne (single JOIN)
posts = Post.objects.select_related('author', 'category').all()

# prefetch_related: ManyToMany, reverse ForeignKey (separate query)
posts = Post.objects.prefetch_related('tags', 'comments').all()

# Combined
posts = Post.objects.select_related('author').prefetch_related('tags').all()

# Custom prefetch
from django.db.models import Prefetch
posts = Post.objects.prefetch_related(
    Prefetch('comments', queryset=Comment.objects.filter(approved=True))
)
```

## Aggregation & Annotation
```python
from django.db.models import Count, Avg, Sum, Max, Min, F

# Aggregate (returns dict)
Post.objects.aggregate(total=Count('id'), avg_views=Avg('view_count'))
# {'total': 100, 'avg_views': 50.5}

# Annotate (per object)
authors = User.objects.annotate(post_count=Count('posts'))
for author in authors:
    print(f"{author.username}: {author.post_count} posts")

# Using F() expressions
Post.objects.update(view_count=F('view_count') + 1)
Post.objects.filter(updated_at__gt=F('created_at'))
```

## Transactions
```python
from django.db import transaction

# Decorator
@transaction.atomic
def transfer_money(from_acc, to_acc, amount):
    from_acc.balance -= amount
    from_acc.save()
    to_acc.balance += amount
    to_acc.save()

# Context manager
def create_order(user, items):
    with transaction.atomic():
        order = Order.objects.create(user=user)
        for item in items:
            OrderItem.objects.create(order=order, **item)
        return order

# Savepoints
with transaction.atomic():
    do_something()
    sid = transaction.savepoint()
    try:
        risky_operation()
    except Exception:
        transaction.savepoint_rollback(sid)
    transaction.savepoint_commit(sid)
```

## 🚨 Gotchas
1. **N+1 queries** - Always use `select_related`/`prefetch_related` for related data
2. **`null=True` on CharField** - Use `blank=True` instead, null creates two "empty" states

---

# 5. Migrations

## Commands
```bash
# Create migrations for all apps
python manage.py makemigrations

# Create for specific app
python manage.py makemigrations blog

# Apply all pending migrations
python manage.py migrate

# Apply specific app
python manage.py migrate blog

# Show migration status
python manage.py showmigrations

# Rollback to specific migration
python manage.py migrate blog 0003_previous

# Create empty migration (for data migrations)
python manage.py makemigrations blog --empty --name populate_slugs

# Squash migrations
python manage.py squashmigrations blog 0001 0010
```

## Data Migration
```python
# blog/migrations/0005_populate_slugs.py
from django.db import migrations
from django.utils.text import slugify

def create_slugs(apps, schema_editor):
    Post = apps.get_model('blog', 'Post')
    for post in Post.objects.filter(slug=''):
        post.slug = slugify(post.title)
        post.save()

def reverse_slugs(apps, schema_editor):
    pass  # Optional reverse

class Migration(migrations.Migration):
    dependencies = [
        ('blog', '0004_add_slug_field'),
    ]
    operations = [
        migrations.RunPython(create_slugs, reverse_slugs),
    ]
```

## 🚨 Gotchas
1. **Migration conflicts** - `python manage.py makemigrations --merge`
2. **Renaming fields** - Django asks, but verify it detects rename vs delete+add

---

# 6. Admin

## Basic Customization
```python
# admin.py
from django.contrib import admin
from .models import Post, Category

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'created_at', 'is_published']
    list_filter = ['is_published', 'created_at', 'category']
    search_fields = ['title', 'content', 'author__username']
    prepopulated_fields = {'slug': ('title',)}
    date_hierarchy = 'created_at'
    ordering = ['-created_at']
    list_editable = ['is_published']
    readonly_fields = ['created_at', 'updated_at']
    raw_id_fields = ['author']  # For large foreign key tables
    
    fieldsets = (
        (None, {'fields': ('title', 'slug', 'content')}),
        ('Publishing', {'fields': ('is_published', 'publish_date'), 'classes': ('collapse',)}),
        ('Metadata', {'fields': ('author', 'category', 'tags')}),
    )
    
    actions = ['make_published', 'make_draft']
    
    @admin.action(description='Mark selected as published')
    def make_published(self, request, queryset):
        updated = queryset.update(is_published=True)
        self.message_user(request, f'{updated} posts published.')

# Inlines
class CommentInline(admin.TabularInline):  # or StackedInline
    model = Comment
    extra = 1

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    inlines = [CommentInline]
```

## 🚨 Gotchas
1. **Forgot `@admin.register`** - Model won't appear in admin
2. **`list_editable` without `list_display`** - Will error

---

# 7. Forms

## Forms vs ModelForms
```python
# forms.py
from django import forms
from .models import Post

# Regular Form (no model)
class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
    
    def clean_email(self):
        email = self.cleaned_data['email']
        if 'spam' in email:
            raise forms.ValidationError('Invalid email')
        return email

# ModelForm (from model)
class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content', 'category', 'tags']
        # Or: exclude = ['author', 'slug']
        widgets = {
            'content': forms.Textarea(attrs={'rows': 10, 'class': 'rich-editor'}),
        }
        labels = {'content': 'Post Body'}
        help_texts = {'title': 'Enter a descriptive title'}
    
    def clean(self):
        cleaned_data = super().clean()
        title = cleaned_data.get('title')
        content = cleaned_data.get('content')
        if title and content and title in content:
            raise forms.ValidationError('Title should not repeat in content')
        return cleaned_data
```

## View Integration
```python
# views.py
def contact_view(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            # Process data
            send_email(form.cleaned_data)
            messages.success(request, 'Message sent!')
            return redirect('contact_success')
    else:
        form = ContactForm()
    return render(request, 'contact.html', {'form': form})

def post_create(request):
    if request.method == 'POST':
        form = PostForm(request.POST, request.FILES)  # FILES for file uploads
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.save()
            form.save_m2m()  # Save ManyToMany after commit=False
            return redirect(post.get_absolute_url())
    else:
        form = PostForm()
    return render(request, 'post_form.html', {'form': form})
```

## Template Rendering
```html
<form method="post" enctype="multipart/form-data">
    {% csrf_token %}
    
    <!-- Auto render all -->
    {{ form.as_p }}
    <!-- Or: {{ form.as_table }}, {{ form.as_div }} -->
    
    <!-- Manual render -->
    {% for field in form %}
        <div class="field {% if field.errors %}has-error{% endif %}">
            {{ field.label_tag }}
            {{ field }}
            {{ field.errors }}
            {% if field.help_text %}<small>{{ field.help_text }}</small>{% endif %}
        </div>
    {% endfor %}
    
    <!-- Non-field errors -->
    {{ form.non_field_errors }}
    
    <button type="submit">Submit</button>
</form>
```

## Formsets
```python
from django.forms import formset_factory, modelformset_factory

# Basic formset
ItemFormSet = formset_factory(ItemForm, extra=3, max_num=10)

# Model formset
PostFormSet = modelformset_factory(Post, fields=['title', 'is_published'], extra=1)

# In view
def manage_posts(request):
    if request.method == 'POST':
        formset = PostFormSet(request.POST, queryset=Post.objects.filter(author=request.user))
        if formset.is_valid():
            formset.save()
            return redirect('posts')
    else:
        formset = PostFormSet(queryset=Post.objects.filter(author=request.user))
    return render(request, 'manage_posts.html', {'formset': formset})
```

## 🚨 Gotchas
1. **Forgot `enctype="multipart/form-data"`** - File uploads silently fail
2. **Forgot `form.save_m2m()`** - ManyToMany fields won't save with `commit=False`

---

# 8. Authentication

## Built-in Auth URLs
```python
# urls.py
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('accounts/', include('django.contrib.auth.urls')),
    # Provides: login, logout, password_change, password_reset, etc.
]

# Or customize:
urlpatterns = [
    path('login/', auth_views.LoginView.as_view(template_name='auth/login.html'), name='login'),
    path('logout/', auth_views.LogoutView.as_view(next_page='/'), name='logout'),
]
```

## Settings
```python
# settings.py
LOGIN_URL = '/accounts/login/'
LOGIN_REDIRECT_URL = '/dashboard/'
LOGOUT_REDIRECT_URL = '/'

# Session settings
SESSION_COOKIE_AGE = 1209600  # 2 weeks
SESSION_EXPIRE_AT_BROWSER_CLOSE = False
```

## Custom User Model (Do This First!)
```python
# accounts/models.py
from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    phone = models.CharField(max_length=20, blank=True)
    avatar = models.ImageField(upload_to='avatars/', blank=True)

# settings.py
AUTH_USER_MODEL = 'accounts.CustomUser'

# Then: makemigrations, migrate
```

## Registration View
```python
# views.py
from django.contrib.auth import login
from django.contrib.auth.forms import UserCreationForm

def register(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            login(request, user)
            return redirect('home')
    else:
        form = UserCreationForm()
    return render(request, 'registration/register.html', {'form': form})
```

## Protecting Views
```python
# FBV
from django.contrib.auth.decorators import login_required, permission_required

@login_required
def dashboard(request):
    return render(request, 'dashboard.html')

@permission_required('blog.add_post', raise_exception=True)
def create_post(request):
    ...

# CBV
from django.contrib.auth.mixins import LoginRequiredMixin, PermissionRequiredMixin

class DashboardView(LoginRequiredMixin, TemplateView):
    template_name = 'dashboard.html'

class CreatePostView(PermissionRequiredMixin, CreateView):
    permission_required = 'blog.add_post'
    ...
```

## Template Auth Context
```html
{% if user.is_authenticated %}
    Welcome, {{ user.username }}!
    <a href="{% url 'logout' %}">Logout</a>
{% else %}
    <a href="{% url 'login' %}">Login</a>
{% endif %}

{% if perms.blog.add_post %}
    <a href="{% url 'post_create' %}">New Post</a>
{% endif %}
```

## 🚨 Gotchas
1. **Custom User after migrations** - Very hard to change later; do it first!
2. **Forgot `AUTH_USER_MODEL`** - Will use default User model

---

# 9. Middleware & Request/Response

## Common Middleware Stack
```python
# settings.py
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',      # Security headers
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',          # URL normalization
    'django.middleware.csrf.CsrfViewMiddleware',          # CSRF protection
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

## Custom Middleware
```python
# middleware.py
import time
import logging

logger = logging.getLogger(__name__)

class RequestTimingMiddleware:
    """Log request processing time"""
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        start = time.time()
        response = self.get_response(request)
        duration = time.time() - start
        logger.info(f'{request.method} {request.path} - {duration:.2f}s')
        return response

class MaintenanceModeMiddleware:
    """Return 503 when in maintenance"""
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        if settings.MAINTENANCE_MODE and not request.user.is_staff:
            return HttpResponse('Site under maintenance', status=503)
        return self.get_response(request)
```

## CSRF Handling
```python
# In templates: {% csrf_token %}

# AJAX with fetch:
const csrftoken = document.querySelector('[name=csrfmiddlewaretoken]').value;
fetch('/api/endpoint/', {
    method: 'POST',
    headers: {'X-CSRFToken': csrftoken},
    body: JSON.stringify(data)
});

# Exempt a view (use sparingly)
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def webhook(request):
    ...
```

## CORS (Cross-Origin)
```python
# Install: pip install django-cors-headers

# settings.py
INSTALLED_APPS = [..., 'corsheaders']
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',  # Before CommonMiddleware
    'django.middleware.common.CommonMiddleware',
    ...
]

CORS_ALLOWED_ORIGINS = [
    'https://frontend.example.com',
]
# Or for dev: CORS_ALLOW_ALL_ORIGINS = True
```

## 🚨 Gotchas
1. **Middleware order matters** - SecurityMiddleware first, CORS before Common
2. **CSRF on AJAX** - Must include token in headers

---

# 10. REST APIs (DRF Add-on)

> Requires: `pip install djangorestframework`

## Setup
```python
# settings.py
INSTALLED_APPS = [..., 'rest_framework']

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.TokenAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 20,
}
```

## Serializers
```python
# serializers.py
from rest_framework import serializers
from .models import Post

class PostSerializer(serializers.ModelSerializer):
    author_name = serializers.CharField(source='author.username', read_only=True)
    
    class Meta:
        model = Post
        fields = ['id', 'title', 'content', 'author', 'author_name', 'created_at']
        read_only_fields = ['author', 'created_at']
    
    def validate_title(self, value):
        if len(value) < 5:
            raise serializers.ValidationError('Title too short')
        return value
```

## ViewSets
```python
# views.py
from rest_framework import viewsets, permissions
from rest_framework.decorators import action
from rest_framework.response import Response

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly]
    
    def perform_create(self, serializer):
        serializer.save(author=self.request.user)
    
    def get_queryset(self):
        qs = super().get_queryset()
        if self.action == 'list':
            return qs.filter(is_published=True)
        return qs
    
    @action(detail=True, methods=['post'])
    def publish(self, request, pk=None):
        post = self.get_object()
        post.is_published = True
        post.save()
        return Response({'status': 'published'})
```

## Routers
```python
# urls.py
from rest_framework.routers import DefaultRouter
from .views import PostViewSet

router = DefaultRouter()
router.register(r'posts', PostViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
]
# Creates: /api/posts/, /api/posts/{pk}/, /api/posts/{pk}/publish/
```

## Authentication
```python
# Token auth setup
INSTALLED_APPS = [..., 'rest_framework.authtoken']
# Then: python manage.py migrate

# Get token endpoint
from rest_framework.authtoken.views import obtain_auth_token
urlpatterns = [
    path('api/token/', obtain_auth_token, name='api_token'),
]

# Usage: Authorization: Token <token>
```

## 🚨 Gotchas
1. **Forgot `rest_framework` in INSTALLED_APPS** - Browsable API breaks
2. **Token vs Session** - Use Session for web, Token for mobile/SPA

---

# 11. Testing

## Django TestCase
```python
# tests/test_models.py
from django.test import TestCase
from django.contrib.auth import get_user_model
from .models import Post

User = get_user_model()

class PostModelTest(TestCase):
    @classmethod
    def setUpTestData(cls):
        """Runs once for the whole test class"""
        cls.user = User.objects.create_user('testuser', 'test@test.com', 'password')
        cls.post = Post.objects.create(title='Test Post', author=cls.user)
    
    def test_post_str(self):
        self.assertEqual(str(self.post), 'Test Post')
    
    def test_get_absolute_url(self):
        self.assertEqual(self.post.get_absolute_url(), f'/posts/{self.post.slug}/')

# tests/test_views.py
from django.test import TestCase, Client
from django.urls import reverse

class PostViewTest(TestCase):
    def setUp(self):
        self.client = Client()
        self.user = User.objects.create_user('testuser', password='password')
        self.post = Post.objects.create(title='Test', author=self.user, is_published=True)
    
    def test_post_list_view(self):
        response = self.client.get(reverse('blog:list'))
        self.assertEqual(response.status_code, 200)
        self.assertContains(response, 'Test')
        self.assertTemplateUsed(response, 'blog/post_list.html')
    
    def test_create_post_requires_login(self):
        response = self.client.get(reverse('blog:create'))
        self.assertRedirects(response, '/accounts/login/?next=/posts/create/')
    
    def test_create_post_authenticated(self):
        self.client.login(username='testuser', password='password')
        response = self.client.post(reverse('blog:create'), {
            'title': 'New Post',
            'content': 'Content here'
        })
        self.assertEqual(response.status_code, 302)  # Redirect on success
        self.assertTrue(Post.objects.filter(title='New Post').exists())
```

## pytest-django (Alternative)
```python
# conftest.py
import pytest
from django.contrib.auth import get_user_model

@pytest.fixture
def user(db):
    return get_user_model().objects.create_user('testuser', password='password')

@pytest.fixture
def authenticated_client(client, user):
    client.login(username='testuser', password='password')
    return client

# test_views.py
import pytest
from django.urls import reverse

@pytest.mark.django_db
def test_post_list(client):
    response = client.get(reverse('blog:list'))
    assert response.status_code == 200

def test_create_post(authenticated_client):
    response = authenticated_client.post(reverse('blog:create'), {'title': 'Test'})
    assert response.status_code == 302
```

## Factory Boy
```python
# factories.py
import factory
from .models import Post, User

class UserFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = User
    username = factory.Sequence(lambda n: f'user{n}')
    email = factory.LazyAttribute(lambda obj: f'{obj.username}@test.com')

class PostFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = Post
    title = factory.Faker('sentence')
    content = factory.Faker('paragraph')
    author = factory.SubFactory(UserFactory)

# Usage in tests
def test_with_factory(self):
    post = PostFactory(title='Custom Title')
    self.assertEqual(post.title, 'Custom Title')
```

## Commands
```bash
python manage.py test                    # Run all tests
python manage.py test blog               # Run app tests
python manage.py test blog.tests.test_views  # Run specific module
python manage.py test --parallel         # Run in parallel
python manage.py test --verbosity=2      # Verbose output

# With coverage
pip install coverage
coverage run --source='.' manage.py test
coverage report
coverage html  # Generate HTML report
```

## 🚨 Gotchas
1. **Test database** - Uses separate DB; data doesn't persist
2. **setUpTestData vs setUp** - Class method runs once, instance runs per test

---

# 12. Security

## Essential Security Settings
```python
# settings.py (production)

# Never expose secret key
SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY')

# Disable debug in production
DEBUG = False

# Restrict allowed hosts
ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com']

# HTTPS settings
SECURE_SSL_REDIRECT = True
SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')

# Cookie security
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_HTTPONLY = True

# HSTS (HTTP Strict Transport Security)
SECURE_HSTS_SECONDS = 31536000  # 1 year
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True

# Content security
SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = 'DENY'

# Referrer policy
SECURE_REFERRER_POLICY = 'strict-origin-when-cross-origin'
```

## CSRF Protection
```python
# All POST forms need CSRF token
# templates/form.html
<form method="post">
    {% csrf_token %}
    {{ form }}
</form>

# AJAX requests - include header
headers: {'X-CSRFToken': getCookie('csrftoken')}

# For APIs (use with caution)
@csrf_exempt
def webhook_endpoint(request): ...
```

## SQL Injection Prevention
```python
# ✅ SAFE - ORM handles escaping
Post.objects.filter(title=user_input)

# ✅ SAFE - Parameterized raw query
Post.objects.raw('SELECT * FROM blog_post WHERE title = %s', [user_input])

# ❌ UNSAFE - String formatting
Post.objects.raw(f'SELECT * FROM blog_post WHERE title = "{user_input}"')
```

## XSS Prevention
```python
# Django auto-escapes template variables
{{ user_input }}  # Safe - auto-escaped

# ❌ Dangerous - only use with trusted content
{{ user_input|safe }}
{% autoescape off %}{{ content }}{% endautoescape %}

# Sanitize user HTML if needed
from django.utils.html import escape, strip_tags
safe_text = escape(user_input)
plain_text = strip_tags(html_content)
```

## Security Check
```bash
# Run Django's security check
python manage.py check --deploy

# Common issues flagged:
# - DEBUG = True
# - Missing HTTPS settings
# - Insecure SECRET_KEY
```

## 🚨 Gotchas
1. **`|safe` filter** - Never use with user input
2. **ALLOWED_HOSTS empty** - Site breaks in production

---

# 13. Performance

## Database Query Optimization
```python
# Avoid N+1 queries
# ❌ Bad - N+1 queries
for post in Post.objects.all():
    print(post.author.username)  # Extra query per post

# ✅ Good - single join
for post in Post.objects.select_related('author'):
    print(post.author.username)

# ✅ Good - prefetch for M2M/reverse FK
for post in Post.objects.prefetch_related('tags'):
    print(list(post.tags.all()))

# Limit fields retrieved
Post.objects.only('title', 'created_at')
Post.objects.defer('content')  # Exclude large fields

# Use exists() and count()
if Post.objects.filter(is_published=True).exists():  # Not: .count() > 0
    ...
```

## Caching
```python
# settings.py - Redis cache
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        'LOCATION': 'redis://127.0.0.1:6379/1',
    }
}

# View caching
from django.views.decorators.cache import cache_page

@cache_page(60 * 15)  # 15 minutes
def post_list(request):
    ...

# Template fragment caching
{% load cache %}
{% cache 500 sidebar request.user.id %}
    ... expensive content ...
{% endcache %}

# Low-level cache API
from django.core.cache import cache

def get_posts():
    posts = cache.get('all_posts')
    if posts is None:
        posts = list(Post.objects.all())
        cache.set('all_posts', posts, 3600)  # 1 hour
    return posts

# Invalidate cache
cache.delete('all_posts')
```

## Pagination
```python
# views.py
from django.core.paginator import Paginator

def post_list(request):
    posts = Post.objects.all()
    paginator = Paginator(posts, 25)  # 25 per page
    page = request.GET.get('page')
    posts = paginator.get_page(page)
    return render(request, 'posts.html', {'posts': posts})

# CBV
class PostListView(ListView):
    model = Post
    paginate_by = 25
```

## Database Indexes
```python
# models.py
class Post(models.Model):
    title = models.CharField(max_length=200, db_index=True)
    
    class Meta:
        indexes = [
            models.Index(fields=['created_at', 'is_published']),
            models.Index(fields=['slug'], name='slug_idx'),
        ]
```

## Async Views (Django 4.1+)
```python
# Async view
async def async_view(request):
    data = await sync_to_async(get_data)()
    return JsonResponse(data)

# Note: ORM is sync - use sync_to_async
from asgiref.sync import sync_to_async

@sync_to_async
def get_posts():
    return list(Post.objects.all())
```

## 🚨 Gotchas
1. **Cache invalidation** - Remember to invalidate when data changes
2. **Async ORM** - Django ORM is sync; must wrap with `sync_to_async`

---

# 14. Deployment

## WSGI vs ASGI
```python
# WSGI - Synchronous (Gunicorn)
# config/wsgi.py
import os
from django.core.wsgi import get_wsgi_application
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings.production')
application = get_wsgi_application()

# ASGI - Async support (Uvicorn/Daphne)
# config/asgi.py
import os
from django.core.asgi import get_asgi_application
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings.production')
application = get_asgi_application()
```

## Gunicorn Configuration
```bash
# Install
pip install gunicorn

# Run
gunicorn config.wsgi:application --bind 0.0.0.0:8000 --workers 3

# With config file (gunicorn.conf.py)
bind = '0.0.0.0:8000'
workers = 3  # (2 * CPU cores) + 1
worker_class = 'sync'  # or 'gevent' for async
timeout = 30
accesslog = '/var/log/gunicorn/access.log'
errorlog = '/var/log/gunicorn/error.log'
```

## Nginx Configuration
```nginx
# /etc/nginx/sites-available/mysite
upstream django {
    server 127.0.0.1:8000;
}

server {
    listen 80;
    server_name yourdomain.com;
    
    # Redirect HTTP to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name yourdomain.com;
    
    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
    
    location /static/ {
        alias /var/www/mysite/staticfiles/;
    }
    
    location /media/ {
        alias /var/www/mysite/media/;
    }
    
    location / {
        proxy_pass http://django;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## Static Files
```bash
# Collect all static files to STATIC_ROOT
python manage.py collectstatic --noinput

# settings.py
STATIC_ROOT = BASE_DIR / 'staticfiles'  # Where collectstatic puts files
STATIC_URL = '/static/'

# For production static serving (whitenoise)
pip install whitenoise
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',  # After SecurityMiddleware
    ...
]
STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
```

## Environment Configuration
```python
# .env file
DJANGO_SECRET_KEY=your-production-secret-key
DJANGO_DEBUG=False
DATABASE_URL=postgres://user:pass@localhost/dbname
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com

# settings.py
import os
from dotenv import load_dotenv
load_dotenv()

SECRET_KEY = os.getenv('DJANGO_SECRET_KEY')
DEBUG = os.getenv('DJANGO_DEBUG', 'False') == 'True'
ALLOWED_HOSTS = os.getenv('ALLOWED_HOSTS', '').split(',')

# Database from URL
import dj_database_url
DATABASES = {'default': dj_database_url.config(default='sqlite:///db.sqlite3')}
```

## Logging Configuration
```python
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'file': {
            'level': 'ERROR',
            'class': 'logging.FileHandler',
            'filename': '/var/log/django/error.log',
            'formatter': 'verbose',
        },
        'console': {
            'class': 'logging.StreamHandler',
            'formatter': 'verbose',
        },
    },
    'root': {
        'handlers': ['console', 'file'],
        'level': 'INFO',
    },
}
```

## Health Check Endpoint
```python
# views.py
from django.http import JsonResponse
from django.db import connection

def health_check(request):
    try:
        with connection.cursor() as cursor:
            cursor.execute('SELECT 1')
        return JsonResponse({'status': 'healthy', 'database': 'ok'})
    except Exception as e:
        return JsonResponse({'status': 'unhealthy', 'error': str(e)}, status=500)

# urls.py
path('health/', views.health_check, name='health_check'),
```

## 🚨 Gotchas
1. **Forgot `collectstatic`** - Static files don't appear in production
2. **DEBUG=True in prod** - Exposes sensitive info and hurts performance

---

# 15. Common Recipes (Top 15)

## 1. Generate Unique Slug
```python
from django.utils.text import slugify
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    slug = models.SlugField(unique=True, blank=True)
    
    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(self.title)
            slug = base_slug
            counter = 1
            while Post.objects.filter(slug=slug).exists():
                slug = f'{base_slug}-{counter}'
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)
```

## 2. Send Email
```python
from django.core.mail import send_mail, EmailMultiAlternatives

# Simple text email
send_mail(
    subject='Welcome',
    message='Thanks for signing up!',
    from_email='noreply@example.com',
    recipient_list=['user@example.com'],
)

# HTML email
email = EmailMultiAlternatives(
    subject='Welcome',
    body='Thanks for signing up!',
    from_email='noreply@example.com',
    to=['user@example.com'],
)
email.attach_alternative('<h1>Welcome!</h1>', 'text/html')
email.send()
```

## 3. Flash Messages
```python
from django.contrib import messages

def my_view(request):
    messages.success(request, 'Operation successful!')
    messages.error(request, 'Something went wrong.')
    return redirect('home')

# In template
{% if messages %}
    {% for message in messages %}
        <div class="alert alert-{{ message.tags }}">{{ message }}</div>
    {% endfor %}
{% endif %}
```

## 4. File Download Response
```python
from django.http import FileResponse, HttpResponse
import os

def download_file(request, filename):
    file_path = os.path.join(settings.MEDIA_ROOT, filename)
    return FileResponse(open(file_path, 'rb'), as_attachment=True)

# Large files
def download_large_file(request):
    response = HttpResponse(content_type='application/octet-stream')
    response['Content-Disposition'] = 'attachment; filename="large.zip"'
    # Stream file in chunks
    with open('/path/to/large.zip', 'rb') as f:
        response.write(f.read())
    return response
```

## 5. Soft Delete
```python
class SoftDeleteManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(deleted_at__isnull=True)

class BaseModel(models.Model):
    deleted_at = models.DateTimeField(null=True, blank=True)
    objects = SoftDeleteManager()
    all_objects = models.Manager()
    
    class Meta:
        abstract = True
    
    def delete(self, *args, **kwargs):
        self.deleted_at = timezone.now()
        self.save()
    
    def hard_delete(self):
        super().delete()
```

## 6. Bulk Create/Update
```python
# Bulk create (much faster than loop)
posts = [Post(title=f'Post {i}', author=user) for i in range(100)]
Post.objects.bulk_create(posts)

# Bulk update
posts = Post.objects.filter(is_published=False)
for post in posts:
    post.is_published = True
Post.objects.bulk_update(posts, ['is_published'])
```

## 7. Get or Create with Defaults
```python
user, created = User.objects.get_or_create(
    username='john',
    defaults={'email': 'john@example.com', 'is_active': True}
)

# Update or create
user, created = User.objects.update_or_create(
    username='john',
    defaults={'last_login': timezone.now()}
)
```

## 8. Custom User Manager
```python
class CustomUserManager(BaseUserManager):
    def create_user(self, email, password=None, **extra_fields):
        if not email:
            raise ValueError('Email is required')
        email = self.normalize_email(email)
        user = self.model(email=email, **extra_fields)
        user.set_password(password)
        user.save()
        return user
    
    def create_superuser(self, email, password=None, **extra_fields):
        extra_fields.setdefault('is_staff', True)
        extra_fields.setdefault('is_superuser', True)
        return self.create_user(email, password, **extra_fields)
```

## 9. JSON Field Queries (Postgres)
```python
from django.db.models import JSONField

class Profile(models.Model):
    data = JSONField(default=dict)

# Query JSON field
Profile.objects.filter(data__settings__theme='dark')
Profile.objects.filter(data__tags__contains=['python'])
```

## 10. Management Command with Progress
```python
from django.core.management.base import BaseCommand
from tqdm import tqdm

class Command(BaseCommand):
    help = 'Process all posts'
    
    def handle(self, *args, **options):
        posts = Post.objects.all()
        for post in tqdm(posts, desc='Processing'):
            # Do something
            pass
        self.stdout.write(self.style.SUCCESS('Done!'))
```

## 11. Signals for Audit Log
```python
from django.db.models.signals import post_save, post_delete
from django.dispatch import receiver

@receiver(post_save, sender=Post)
def log_post_save(sender, instance, created, **kwargs):
    action = 'created' if created else 'updated'
    AuditLog.objects.create(
        model=sender.__name__,
        object_id=instance.pk,
        action=action,
        user=instance.author
    )
```

## 12. Rate Limiting View
```python
from django.core.cache import cache
from django.http import HttpResponseTooManyRequests

def rate_limit(key, limit=10, period=60):
    def decorator(view_func):
        def wrapper(request, *args, **kwargs):
            cache_key = f'rate_limit:{key}:{request.META.get("REMOTE_ADDR")}'
            count = cache.get(cache_key, 0)
            if count >= limit:
                return HttpResponseTooManyRequests('Rate limited')
            cache.set(cache_key, count + 1, period)
            return view_func(request, *args, **kwargs)
        return wrapper
    return decorator

@rate_limit('api', limit=100, period=3600)
def api_view(request): ...
```

## 13. Export to CSV
```python
import csv
from django.http import HttpResponse

def export_posts_csv(request):
    response = HttpResponse(content_type='text/csv')
    response['Content-Disposition'] = 'attachment; filename="posts.csv"'
    
    writer = csv.writer(response)
    writer.writerow(['Title', 'Author', 'Created'])
    
    for post in Post.objects.all():
        writer.writerow([post.title, post.author.username, post.created_at])
    
    return response
```

## 14. Scheduled Tasks (Celery Beat)
```python
# celery.py
app.conf.beat_schedule = {
    'daily-cleanup': {
        'task': 'myapp.tasks.cleanup_old_data',
        'schedule': crontab(hour=0, minute=0),  # Midnight
    },
}

# tasks.py
@shared_task
def cleanup_old_data():
    cutoff = timezone.now() - timedelta(days=30)
    Post.objects.filter(deleted_at__lt=cutoff).delete()
```

## 15. Webhook Handling
```python
import hmac
import hashlib
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def webhook(request):
    signature = request.headers.get('X-Signature')
    expected = hmac.new(
        settings.WEBHOOK_SECRET.encode(),
        request.body,
        hashlib.sha256
    ).hexdigest()
    
    if not hmac.compare_digest(signature, expected):
        return HttpResponse('Invalid signature', status=403)
    
    data = json.loads(request.body)
    # Process webhook
    return HttpResponse('OK')
```

---

# 16. Troubleshooting

## Common Errors and Fixes

### AppRegistryNotReady
```python
# Error: django.core.exceptions.AppRegistryNotReady: Apps aren't loaded yet

# Fix: Call django.setup() before importing models
import django
django.setup()
from myapp.models import Post
```

### DisallowedHost
```python
# Error: Invalid HTTP_HOST header: 'example.com'. You may need to add 'example.com' to ALLOWED_HOSTS.

# Fix: Add domain to ALLOWED_HOSTS
ALLOWED_HOSTS = ['example.com', 'www.example.com', 'localhost']
```

### Migration Conflicts
```bash
# Error: Conflicting migrations detected

# Fix: Merge migrations
python manage.py makemigrations --merge

# Or delete conflicting migrations and recreate
```

### Static Files Not Loading
```bash
# 1. Check STATIC_URL and STATIC_ROOT
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'

# 2. Run collectstatic
python manage.py collectstatic

# 3. In development, ensure DEBUG=True or add to urls.py
if settings.DEBUG:
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATICFILES_DIRS[0])

# 4. In production, use whitenoise or nginx
```

### Template Not Found
```python
# Check TEMPLATES configuration
TEMPLATES = [{
    'DIRS': [BASE_DIR / 'templates'],  # Project-level templates
    'APP_DIRS': True,  # Enable app template directories
}]

# File should be at: templates/app/template.html or app/templates/app/template.html
```

### CSRF Verification Failed
```html
<!-- Include CSRF token in forms -->
<form method="post">
    {% csrf_token %}
    ...
</form>

<!-- For AJAX, include header -->
headers: {'X-CSRFToken': getCookie('csrftoken')}
```

### Database Connection Errors
```python
# Check DATABASE settings
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'dbname',
        'USER': 'user',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

# Test connection
python manage.py dbshell
```

### ImportError: No module named
```bash
# Check virtual environment is activated
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Check package is installed
pip list | grep django
pip install package-name
```

### Reverse for 'view' not found
```python
# 1. Check URL name exists
path('posts/', views.post_list, name='post_list'),  # Has name

# 2. Check namespace in include
path('blog/', include('blog.urls', namespace='blog')),

# 3. Use correct namespace in template
{% url 'blog:post_list' %}
```

### Model has no attribute 'objects'
```python
# Ensure you're using the model class, not an instance
Post.objects.all()  # Correct
post.objects.all()  # Wrong - 'post' is an instance
```

## Debug Checklist
```text
[ ] Check error message carefully
[ ] Verify DEBUG = True shows full traceback
[ ] Check logs: /var/log/django/ or console
[ ] Verify migrations are applied: python manage.py showmigrations
[ ] Check database connectivity
[ ] Verify virtual environment is activated
[ ] Check static files: python manage.py findstatic filename
[ ] Clear cache: cache.clear()
[ ] Restart server after code changes
```

---

> **📖 End of Cheat Sheet** - Bookmark this for quick reference during Django development!

> **Prompt used** 
"""Create a comprehensive Django cheat sheet for quick reference (Django 4.x/5.x). Cover the full “day-to-day” developer workflow from project setup to deployment.

Requirements:
- Organize by sections with clear headings and short bullet points.
- For each topic include: what it is, when to use it, minimal example, and 1–2 gotchas.
- Include commands and code snippets that are copy-paste friendly.
- Must cover:
  - Project/app setup: startproject/startapp, settings structure, environment variables, secrets management.
  - URLs & views: FBV vs CBV, path/re_path, URL namespaces, class-based generic views patterns.
  - Templates: inheritance, filters/tags, context processors, static/media, template debugging.
  - Models & ORM: field types, relations, query patterns, select_related/prefetch_related, annotations, transactions, constraints, indexes.
  - Migrations: makemigrations/migrate, squashing, data migrations, migration conflicts.
  - Admin: customization, inlines, list_display/search/filter, actions, permissions.
  - Forms: forms vs modelforms, validation, formsets, crispy-forms mention (optional).
  - Auth: users, custom user model, permissions/groups, login/logout, password reset, sessions.
  - Middleware & request/response: common middleware patterns, headers, CSRF/CORS basics.
  - REST APIs: Django REST Framework essentials (serializers, viewsets, routers, auth, pagination) OR clearly mark as “DRF add-on”.
  - Testing: TestCase vs pytest-django, factories, client, mocking, coverage.
  - Security: CSRF, XSS, SQL injection prevention, security settings (SECURE_*), allowed hosts.
  - Performance: caching, query optimization, pagination, static files, async views basics (limits).
  - Deployment: WSGI/ASGI, Gunicorn/Uvicorn, Nginx, collectstatic, environment config, logging, health checks.
  - Troubleshooting: common errors and fixes (e.g., AppRegistryNotReady, DisallowedHost, migration issues, static not loading).
- Provide a “Common recipes” section (top 15 tasks) and a “Troubleshooting” section.
- Output in Markdown.

Optional:
- Add a one-page “printable” condensed version at the top.
- Include a mini checklist for production readiness.

Assumptions:
- Use Postgres examples where DB-specific behavior matters, otherwise stay database-agnostic.
- Prefer Django built-ins over third-party packages; mention common packages only when clearly beneficial."""