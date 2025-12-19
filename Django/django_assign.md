# 🐍 Django Framework Mastery Curriculum

> **A Progressive Learning Path from Beginner to Production-Ready Developer**

This comprehensive curriculum contains **70 hands-on assignments** organized across 4 proficiency levels. Each assignment builds upon previous ones to systematically develop production-ready Django skills.

---

## 📋 Curriculum Overview

| Level | Assignments | Focus Areas |
|-------|-------------|-------------|
| 🟢 **Beginner** | B01-B18 | Django fundamentals, views, URLs, templates, settings |
| 🟡 **Intermediate** | I01-I20 | Models, ORM, forms, authentication, class-based views |
| 🟠 **Advanced** | A01-A18 | REST APIs, testing, middleware, custom commands |
| 🔴 **Expert** | E01-E14 | Performance, security, deployment, production patterns |

---

## 🎯 How to Use This Curriculum

1. **Complete assignments in order** - Each builds on concepts from previous ones
2. **Use difficulty indicators**:
   - ⭐ Easy (< 1 hour)
   - ⭐⭐ Moderate (1-2 hours)
   - ⭐⭐⭐ Challenging (2-4 hours)
   - ⭐⭐⭐⭐ Complex (4+ hours)
3. **Check all deliverables** before moving to the next assignment
4. **Build the capstone project** incrementally throughout the curriculum

---

# 🟢 BEGINNER LEVEL (B01-B18)

*Focus: Django fundamentals, project structure, views, URLs, templates, and settings*

---

## B01: Environment Setup and First Django Project ⭐

**Learning Objectives:**
- Set up a Python virtual environment for Django development
- Install Django and understand version management
- Create and run a Django project
- Navigate Django's default project structure

**Requirements:**
1. Create a virtual environment using `venv`
2. Install Django using pip with version pinning
3. Create a new Django project called `mysite`
4. Run the development server and verify it works
5. Document all commands used in a `setup_notes.md`

**Deliverables:**
- Working virtual environment with Django installed
- Running Django development server
- `setup_notes.md` with installation commands and explanations
- Screenshot of the Django welcome page

**Concepts to Implement:**
- `python -m venv`
- `pip install django==X.Y`
- `django-admin startproject`
- `python manage.py runserver`

---

## B02: Understanding Project Structure ⭐

**Learning Objectives:**
- Understand the purpose of each file in a Django project
- Distinguish between project and application concepts
- Create your first Django application

**Requirements:**
1. Document the purpose of:
   - `manage.py`
   - `settings.py`
   - `urls.py`
   - `wsgi.py` / `asgi.py`
2. Create a Django app called `pages`
3. Register the app in `INSTALLED_APPS`
4. Create a `README.md` explaining project vs. app distinction

**Deliverables:**
- `pages` app created and registered
- `README.md` with detailed explanations of each file
- Verification that the app is properly configured

**Concepts to Implement:**
- `python manage.py startapp`
- `INSTALLED_APPS` configuration
- Django's modular architecture

---

## B03: Your First View and URL Pattern ⭐

**Learning Objectives:**
- Create a function-based view (FBV)
- Map URLs to views using URLconf
- Understand request/response cycle

**Requirements:**
1. Create a view function that returns "Hello, Django!"
2. Create a `urls.py` in the `pages` app
3. Include the app's URLs in the project's main `urls.py`
4. Access the view at `/hello/`

**Deliverables:**
- Working view function in `pages/views.py`
- App-level `pages/urls.py` with URL pattern
- Updated project `urls.py` using `include()`
- Browser verification of the route

**Concepts to Implement:**
- `HttpResponse`
- `path()` function
- `include()` for app URLs
- URL namespacing

---

## B04: Multiple Views and URL Parameters ⭐⭐

**Learning Objectives:**
- Create multiple views in a single app
- Pass parameters through URLs
- Use path converters for type validation

**Requirements:**
1. Create a home page view at `/`
2. Create an about page view at `/about/`
3. Create a dynamic greeting view at `/greet/<name>/`
4. Create a view that accepts a number at `/square/<int:num>/` and returns its square

**Deliverables:**
- Four working view functions
- URL patterns with path converters (`str`, `int`)
- Verified responses for all routes

**Concepts to Implement:**
- Multiple `path()` entries
- `<str:name>` and `<int:num>` converters
- Dynamic URL routing

---

## B05: Introduction to Templates ⭐⭐

**Learning Objectives:**
- Set up Django template configuration
- Create and render HTML templates
- Pass context data to templates

**Requirements:**
1. Create a `templates` directory in your app
2. Configure `TEMPLATES` in settings.py
3. Create `home.html` with proper HTML structure
4. Render the template from a view with context data

**Deliverables:**
- `templates/pages/home.html` with basic HTML
- Updated `settings.py` template configuration
- View that renders template with context
- Page displaying dynamic data from context

**Concepts to Implement:**
- `render()` shortcut
- Template directory structure
- Context dictionaries
- Basic HTML templating

---

## B06: Template Language Fundamentals ⭐⭐

**Learning Objectives:**
- Use Django template variables and filters
- Implement template tags for logic
- Apply built-in filters for data formatting

**Requirements:**
1. Display variables using `{{ variable }}`
2. Use `{% if %}` for conditional rendering
3. Use `{% for %}` to iterate over a list
4. Apply filters: `|lower`, `|upper`, `|date`, `|length`
5. Create a page that displays a list of items with conditional styling

**Deliverables:**
- Template using all required tags and filters
- View passing complex context (lists, dicts, dates)
- Demonstration of conditional rendering

**Concepts to Implement:**
- Template variables `{{ }}`
- Template tags `{% %}`
- Built-in filters
- `{% empty %}` for empty lists

---

## B07: Template Inheritance and Blocks ⭐⭐

**Learning Objectives:**
- Create a base template for consistency
- Use template inheritance with `extends`
- Define reusable blocks

**Requirements:**
1. Create `base.html` with common HTML structure
2. Define `{% block title %}`, `{% block content %}`, and `{% block extra_css %}`
3. Create child templates that extend `base.html`
4. Implement a consistent navigation across all pages

**Deliverables:**
- `templates/base.html` with defined blocks
- At least 3 child templates extending the base
- Consistent navigation and footer
- Proper use of `{% block %}` and `{% extends %}`

**Concepts to Implement:**
- `{% extends "base.html" %}`
- `{% block name %}{% endblock %}`
- `{{ block.super }}`
- Template inheritance hierarchy

---

## B08: Static Files Configuration ⭐⭐

**Learning Objectives:**
- Configure Django to serve static files
- Organize CSS, JavaScript, and images
- Use the `{% static %}` template tag

**Requirements:**
1. Create `static/pages/css/style.css`
2. Create `static/pages/js/main.js`
3. Add an image to `static/pages/images/`
4. Configure `STATIC_URL` and `STATICFILES_DIRS`
5. Link static files in templates using `{% static %}`

**Deliverables:**
- Properly organized static file directory
- CSS styling applied to templates
- JavaScript file loaded and executing
- Image displayed using `{% static %}` tag

**Concepts to Implement:**
- `STATIC_URL` and `STATICFILES_DIRS`
- `{% load static %}`
- `{% static 'path/to/file' %}`
- Static file organization patterns

---

## B09: Django Settings Deep Dive ⭐⭐

**Learning Objectives:**
- Understand all core settings in `settings.py`
- Configure debug mode and allowed hosts
- Set up logging configuration

**Requirements:**
1. Document each setting in `settings.py` with explanations
2. Configure `DEBUG` and `ALLOWED_HOSTS` for development
3. Set up basic logging to file
4. Configure timezone and language settings
5. Create environment-specific settings structure

**Deliverables:**
- Annotated `settings.py` with comments
- Working logging configuration
- `settings/` directory with `base.py`, `development.py`, `production.py`
- Environment variable usage for sensitive settings

**Concepts to Implement:**
- `DEBUG`, `ALLOWED_HOSTS`
- `LOGGING` configuration
- `TIME_ZONE`, `LANGUAGE_CODE`
- Settings module splitting

---

## B10: URL Naming and Reversing ⭐⭐

**Learning Objectives:**
- Name URL patterns for reference
- Use `reverse()` and `{% url %}` for dynamic URLs
- Implement app namespacing

**Requirements:**
1. Add names to all existing URL patterns
2. Use `{% url 'name' %}` in templates for navigation
3. Use `reverse()` in views for redirects
4. Implement app namespacing with `app_name`

**Deliverables:**
- All URLs properly named
- Navigation using `{% url %}` tags exclusively
- View using `reverse()` for redirects
- App namespace implemented

**Concepts to Implement:**
- `path(..., name='view_name')`
- `{% url 'app:view_name' %}`
- `reverse('app:view_name')`
- `app_name` in urls.py

---

## B11: HTTP Methods and Request Object ⭐⭐

**Learning Objectives:**
- Understand the HTTP request object
- Handle different HTTP methods
- Access request data (GET, POST, headers)

**Requirements:**
1. Create a view that handles both GET and POST requests
2. Access and display GET query parameters
3. Access request headers and display user-agent
4. Implement a simple search form using GET method

**Deliverables:**
- View handling multiple HTTP methods
- Template with search form
- Display of request metadata
- Query parameter handling demonstration

**Concepts to Implement:**
- `request.method`
- `request.GET` and `request.POST`
- `request.META`
- HTTP method handling

---

## B12: Response Types and Status Codes ⭐⭐

**Learning Objectives:**
- Return different response types
- Set custom status codes
- Return JSON responses

**Requirements:**
1. Return plain text with content type
2. Return JSON data from a view
3. Return custom status codes (201, 400, 404)
4. Implement a custom 404 page
5. Redirect to another view

**Deliverables:**
- Views returning different content types
- JSON API endpoint
- Custom error pages (`404.html`, `500.html`)
- Working redirect implementation

**Concepts to Implement:**
- `HttpResponse` with content_type
- `JsonResponse`
- `HttpResponseNotFound`, `Http404`
- `redirect()` shortcut

---

## B13: Template Includes and Partials ⭐

**Learning Objectives:**
- Create reusable template partials
- Use `{% include %}` for modularity
- Pass context to included templates

**Requirements:**
1. Create `_navbar.html` partial template
2. Create `_footer.html` partial template
3. Create `_card.html` component template
4. Include partials in base template
5. Pass custom context to included templates

**Deliverables:**
- At least 3 partial templates with `_` prefix naming
- Base template using `{% include %}`
- Demonstration of context passing to partials
- Reusable card component used in multiple pages

**Concepts to Implement:**
- `{% include '_partial.html' %}`
- `{% include '_partial.html' with var=value %}`
- Naming conventions for partials
- Template composition

---

## B14: Custom Template Tags (Simple) ⭐⭐⭐

**Learning Objectives:**
- Create simple custom template tags
- Register tags with the template library
- Use custom tags in templates

**Requirements:**
1. Create `templatetags/` directory in your app
2. Create a simple tag that returns current year
3. Create an inclusion tag for a navigation menu
4. Create a simple filter for text formatting

**Deliverables:**
- `templatetags/custom_tags.py` with registered tags
- Template using custom tags
- Documentation for each custom tag

**Concepts to Implement:**
- `@register.simple_tag`
- `@register.inclusion_tag`
- `@register.filter`
- `{% load custom_tags %}`

---

## B15: Managing Multiple Apps ⭐⭐

**Learning Objectives:**
- Structure a project with multiple apps
- Configure app-specific URLs
- Share templates between apps

**Requirements:**
1. Create a second app called `blog` for blog functionality
2. Create a third app called `contact` for contact forms
3. Set up URL routing for each app
4. Create a project-level templates directory
5. Organize static files per app

**Deliverables:**
- Three apps: `pages`, `blog`, `contact`
- Each app with its own `urls.py`
- Project-level and app-level templates
- Clean separation of concerns

**Concepts to Implement:**
- Multi-app architecture
- URL namespacing per app
- Template directory hierarchy
- Static files per app

---

## B16: Context Processors ⭐⭐⭐

**Learning Objectives:**
- Understand built-in context processors
- Create custom context processors
- Make data available in all templates

**Requirements:**
1. Create a context processor that adds site settings to all templates
2. Create a context processor that adds current year
3. Register context processors in settings
4. Use context processor data in base template

**Deliverables:**
- `context_processors.py` with custom processors
- Updated `TEMPLATES` settings
- Base template using context processor data
- Documentation of built-in context processors

**Concepts to Implement:**
- Custom context processor functions
- `TEMPLATES['OPTIONS']['context_processors']`
- Global template variables
- Request-aware context processors

---

## B17: Serving Error Pages ⭐⭐

**Learning Objectives:**
- Create custom error page templates
- Handle 404 and 500 errors gracefully
- Debug error handling

**Requirements:**
1. Create `templates/404.html` with user-friendly design
2. Create `templates/500.html` with user-friendly design
3. Create `templates/403.html` for permission denied
4. Test error pages with `DEBUG=False`
5. Add helpful links and search on error pages

**Deliverables:**
- Custom error templates (404, 500, 403)
- Error pages matching site design
- Tested with DEBUG mode off
- Helpful navigation on error pages

**Concepts to Implement:**
- Error template naming conventions
- `handler404`, `handler500` in urls.py
- DEBUG mode configuration
- User-friendly error handling

---

## B18: Beginner Capstone - Personal Portfolio Site ⭐⭐⭐⭐

**Learning Objectives:**
- Apply all beginner concepts in a complete project
- Build a multi-page website from scratch
- Implement proper project structure

**Requirements:**
1. Create a portfolio site with:
   - Home page with introduction
   - About page with bio
   - Projects page with project cards
   - Contact page with form (no backend yet)
2. Use template inheritance throughout
3. Implement consistent navigation
4. Style with CSS and include images
5. Use URL naming and reversing

**Deliverables:**
- Complete portfolio site with 4+ pages
- Base template with navigation and footer
- Responsive CSS styling
- Static files properly served
- Clean URL structure with names
- README with project documentation

**Concepts to Implement:**
- All concepts from B01-B17
- Project organization
- Template inheritance
- Static files
- URL patterns and naming

---

# 🟡 INTERMEDIATE LEVEL (I01-I20)

*Focus: Models, ORM, database operations, forms, authentication, and class-based views*

---

## I01: Introduction to Django Models ⭐⭐

**Learning Objectives:**
- Define Django models with fields
- Understand field types and options
- Create and apply migrations

**Requirements:**
1. Create a `BlogPost` model with:
   - `title` (CharField, max 200)
   - `content` (TextField)
   - `created_at` (DateTimeField, auto)
   - `updated_at` (DateTimeField, auto)
   - `is_published` (BooleanField)
2. Create and apply migrations
3. Register model in admin
4. Create sample data via admin

**Deliverables:**
- `blog/models.py` with BlogPost model
- Migration files generated and applied
- Model registered in `admin.py`
- Sample blog posts created

**Concepts to Implement:**
- Model class definition
- Field types and arguments
- `makemigrations` and `migrate`
- `__str__` method

---

## I02: Django Admin Customization ⭐⭐

**Learning Objectives:**
- Customize admin interface for models
- Add filters, search, and list display
- Create admin actions

**Requirements:**
1. Create `ModelAdmin` class for BlogPost
2. Configure `list_display`, `list_filter`, `search_fields`
3. Add `date_hierarchy` for created_at
4. Create a custom admin action to publish posts
5. Make fields read-only in admin

**Deliverables:**
- Customized admin for BlogPost
- Search and filter functionality
- Custom admin action
- Read-only and editable field configuration

**Concepts to Implement:**
- `@admin.register` decorator
- `list_display`, `list_filter`
- `search_fields`, `date_hierarchy`
- `actions` and `readonly_fields`

---

## I03: Model Field Types Deep Dive ⭐⭐

**Learning Objectives:**
- Use various Django field types
- Understand field options and validators
- Implement choices and defaults

**Requirements:**
1. Create an `Author` model with:
   - `name` (CharField)
   - `email` (EmailField, unique)
   - `bio` (TextField, optional)
   - `website` (URLField, optional)
   - `avatar` (ImageField, optional)
   - `status` (CharField with choices: active/inactive)
   - `created_at` (DateTimeField)
2. Install and configure Pillow for ImageField
3. Add field validators

**Deliverables:**
- Author model with diverse field types
- Choices implementation
- Field validators applied
- Pillow configured for image handling

**Concepts to Implement:**
- `EmailField`, `URLField`, `ImageField`
- `choices` parameter
- `blank=True`, `null=True`
- Field validators

---

## I04: Model Relationships - ForeignKey ⭐⭐⭐

**Learning Objectives:**
- Implement one-to-many relationships
- Use ForeignKey field properly
- Understand related_name and on_delete

**Requirements:**
1. Add ForeignKey from BlogPost to Author
2. Configure `on_delete` behavior appropriately
3. Set `related_name` for reverse queries
4. Create views showing posts by author
5. Update admin to show related posts

**Deliverables:**
- BlogPost with author ForeignKey
- Migration for the relationship
- View showing author's posts
- Admin inline for posts

**Concepts to Implement:**
- `ForeignKey(Model, on_delete=...)`
- `related_name` for reverse access
- `on_delete` options (CASCADE, SET_NULL, PROTECT)
- Admin inlines

---

## I05: Model Relationships - ManyToMany ⭐⭐⭐

**Learning Objectives:**
- Implement many-to-many relationships
- Use through models for extra data
- Query many-to-many relationships

**Requirements:**
1. Create a `Tag` model with name and slug
2. Add ManyToManyField to BlogPost for tags
3. Create a through model to add ordering
4. Implement views for filtering by tag
5. Display tags on posts

**Deliverables:**
- Tag model with ManyToMany relationship
- Through model with extra fields
- Tag filtering in views
- Tags displayed on post templates

**Concepts to Implement:**
- `ManyToManyField`
- `through` parameter
- `add()`, `remove()`, `clear()` methods
- Filtering with many-to-many

---

## I06: Django ORM Queries ⭐⭐⭐

**Learning Objectives:**
- Master QuerySet methods
- Filter, exclude, and order querysets
- Use Q objects for complex queries

**Requirements:**
1. Implement filtering: `filter()`, `exclude()`, `get()`
2. Use field lookups: `__gte`, `__contains`, `__iexact`
3. Order querysets with `order_by()`
4. Chain queries and use `Q` objects for OR conditions
5. Create a search view with multiple filters

**Deliverables:**
- View with advanced filtering
- Complex queries using Q objects
- Search functionality with multiple criteria
- Demonstration of all lookup types

**Concepts to Implement:**
- `filter()`, `exclude()`, `get()`
- Field lookups (`__gte`, `__lte`, `__contains`, `__in`)
- `Q` objects for complex queries
- `order_by()`, `reverse()`

---

## I07: QuerySet Aggregation and Annotation ⭐⭐⭐

**Learning Objectives:**
- Use aggregation functions
- Annotate querysets with calculated values
- Group data for statistics

**Requirements:**
1. Count posts per author using `annotate()`
2. Calculate average, max, min with aggregation
3. Use `values()` and `annotate()` for grouping
4. Create a statistics dashboard view
5. Display author statistics with post counts

**Deliverables:**
- Views using aggregation functions
- Statistics dashboard template
- Author listing with post counts
- Performance-optimized queries

**Concepts to Implement:**
- `aggregate()` with Count, Avg, Sum, Max, Min
- `annotate()` for per-object calculations
- `values()` for grouping
- `F` expressions

---

## I08: Model Methods and Properties ⭐⭐

**Learning Objectives:**
- Add custom methods to models
- Use `@property` decorators
- Implement model managers

**Requirements:**
1. Add methods to BlogPost:
   - `get_excerpt()` - returns first 100 chars
   - `get_absolute_url()` - returns post URL
   - `is_recent()` - returns True if < 7 days old
2. Add `@property` for word count
3. Create custom manager with `published()` method

**Deliverables:**
- Model with custom methods
- Properties for computed values
- Custom manager with convenience methods
- Templates using model methods

**Concepts to Implement:**
- Instance methods on models
- `@property` decorator
- `get_absolute_url()`
- Custom managers

---

## I09: Django Forms Basics ⭐⭐

**Learning Objectives:**
- Create forms using Django Forms
- Render forms in templates
- Handle form submission and validation

**Requirements:**
1. Create `ContactForm` with name, email, message fields
2. Create view to display and process form
3. Render form in template with CSRF token
4. Display validation errors
5. Show success message on submission

**Deliverables:**
- `forms.py` with ContactForm
- View handling GET and POST
- Template with form rendering
- Error display and success messages

**Concepts to Implement:**
- `forms.Form` class
- Form fields and validation
- `{% csrf_token %}`
- `form.is_valid()`, `form.cleaned_data`

---

## I10: ModelForms ⭐⭐

**Learning Objectives:**
- Create forms from models automatically
- Customize ModelForm behavior
- Save form data to database

**Requirements:**
1. Create `BlogPostForm` from BlogPost model
2. Exclude or include specific fields
3. Add custom validation in form
4. Create view to add new blog post
5. Create view to edit existing blog post

**Deliverables:**
- `BlogPostForm` ModelForm
- Create and update views
- Forms with custom validation
- Success redirects after save

**Concepts to Implement:**
- `forms.ModelForm`
- `Meta` class with `model`, `fields`, `exclude`
- `clean_<fieldname>()` methods
- `form.save()`

---

## I11: Form Widgets and Rendering ⭐⭐

**Learning Objectives:**
- Customize form field widgets
- Control form rendering in templates
- Add CSS classes to form fields

**Requirements:**
1. Customize widgets for each field type
2. Add CSS classes and attributes to widgets
3. Render forms manually field by field
4. Use crispy-forms or similar for styling
5. Create reusable form templates

**Deliverables:**
- Forms with custom widgets
- Manual form rendering template
- Styled forms with CSS framework
- Reusable form partial templates

**Concepts to Implement:**
- `widgets` in Meta class
- `attrs` dictionary for widgets
- Manual field rendering
- Form template customization

---

## I12: Form Validation Advanced ⭐⭐⭐

**Learning Objectives:**
- Implement custom validation logic
- Create cross-field validation
- Use built-in validators

**Requirements:**
1. Add custom `clean_<field>()` methods
2. Implement `clean()` for cross-field validation
3. Use validators: `MinLengthValidator`, `RegexValidator`
4. Create a registration form with:
   - Password confirmation matching
   - Email uniqueness check
   - Strong password validation

**Deliverables:**
- Form with custom field validation
- Cross-field validation implementation
- Registration form with all validators
- Clear error messages

**Concepts to Implement:**
- `clean_fieldname()` methods
- `clean()` method override
- `validators` parameter
- `ValidationError`

---

## I13: User Authentication Setup ⭐⭐⭐

**Learning Objectives:**
- Configure Django's authentication system
- Create login, logout, and register views
- Use authentication decorators

**Requirements:**
1. Configure authentication URLs
2. Create custom login template
3. Create registration view with form
4. Implement logout functionality
5. Display user-specific content on templates

**Deliverables:**
- Working login/logout system
- Registration with email verification (optional)
- Protected views with `@login_required`
- User-aware templates

**Concepts to Implement:**
- `django.contrib.auth.urls`
- Custom auth templates in `registration/`
- `@login_required` decorator
- `{{ user }}` in templates

---

## I14: User Profile Extension ⭐⭐⭐

**Learning Objectives:**
- Extend the User model with a profile
- Use signals for automatic profile creation
- Create profile views and forms

**Requirements:**
1. Create `UserProfile` model with:
   - OneToOne link to User
   - Bio, avatar, website fields
2. Create signal to auto-create profile
3. Create profile view and update form
4. Display profile information on user pages

**Deliverables:**
- UserProfile model with signals
- Profile view and edit form
- Signal for automatic profile creation
- Profile display templates

**Concepts to Implement:**
- `OneToOneField` to User
- `@receiver(post_save, sender=User)`
- Profile form handling
- Related object access

---

## I15: Permissions and Authorization ⭐⭐⭐

**Learning Objectives:**
- Understand Django's permission system
- Create and check custom permissions
- Implement group-based permissions

**Requirements:**
1. Add custom permissions to BlogPost model
2. Check permissions in views
3. Create editor group with specific permissions
4. Use `@permission_required` decorator
5. Display content based on permissions

**Deliverables:**
- Model with custom permissions in Meta
- Views with permission checks
- Groups with assigned permissions
- Permission-based template content

**Concepts to Implement:**
- `Meta.permissions`
- `@permission_required`
- `user.has_perm()`
- Group permissions

---

## I16: Class-Based Views Introduction ⭐⭐

**Learning Objectives:**
- Understand CBV fundamentals
- Convert FBVs to CBVs
- Use View and TemplateView

**Requirements:**
1. Convert home page FBV to TemplateView
2. Create a View with get and post methods
3. Add extra context to CBVs
4. Use `as_view()` in URL patterns
5. Document differences between FBV and CBV

**Deliverables:**
- Home page using TemplateView
- Custom View with HTTP method handlers
- Documented FBV vs CBV comparison
- Working URL configuration

**Concepts to Implement:**
- `View` and `TemplateView`
- `get()`, `post()` methods
- `get_context_data()`
- `as_view()`

---

## I17: Generic Display Views ⭐⭐

**Learning Objectives:**
- Use ListView for object lists
- Use DetailView for single objects
- Customize generic views

**Requirements:**
1. Create BlogPost ListView at `/posts/`
2. Create BlogPost DetailView at `/posts/<slug>/`
3. Add pagination to ListView
4. Filter ListView with query parameters
5. Add slug field to BlogPost model

**Deliverables:**
- Working ListView with pagination
- DetailView with slug lookup
- Templates for list and detail
- Query-based filtering in ListView

**Concepts to Implement:**
- `ListView`, `DetailView`
- `paginate_by`, `template_name`
- `get_queryset()`, `get_object()`
- Slug-based URLs

---

## I18: Generic Edit Views ⭐⭐⭐

**Learning Objectives:**
- Use CreateView, UpdateView, DeleteView
- Configure form handling in CBVs
- Implement success URL patterns

**Requirements:**
1. Create BlogPost creation view at `/posts/new/`
2. Create update view at `/posts/<slug>/edit/`
3. Create delete view with confirmation
4. Restrict views to authenticated users
5. Set success URLs dynamically

**Deliverables:**
- Working CRUD views for BlogPost
- Login required for edit/delete
- Delete confirmation template
- Success redirects to detail page

**Concepts to Implement:**
- `CreateView`, `UpdateView`, `DeleteView`
- `LoginRequiredMixin`
- `success_url` and `get_success_url()`
- Form validation in CBVs

---

## I19: Mixins and View Customization ⭐⭐⭐

**Learning Objectives:**
- Understand multiple inheritance in CBVs
- Create custom mixins
- Combine mixins for complex behavior

**Requirements:**
1. Create `OwnerRequiredMixin` for object ownership
2. Create `StaffRequiredMixin` for staff-only views
3. Use `LoginRequiredMixin` with views
4. Combine multiple mixins in views
5. Document mixin order importance

**Deliverables:**
- Custom mixins in `mixins.py`
- Views using multiple mixins
- Ownership-based access control
- Documentation of MRO (Method Resolution Order)

**Concepts to Implement:**
- Custom mixin classes
- Mixin inheritance order
- `dispatch()` method
- `get_queryset()` filtering

---

## I20: Intermediate Capstone - Blog Application ⭐⭐⭐⭐

**Learning Objectives:**
- Apply all intermediate concepts
- Build a complete blog with CRUD
- Implement users and permissions

**Requirements:**
1. Complete blog application with:
   - User registration and authentication
   - BlogPost CRUD with ownership
   - Tags with filtering
   - Author profiles
   - Comment system
   - Admin customization
2. Use CBVs throughout
3. Implement proper permissions
4. Add pagination and search

**Deliverables:**
- Complete blog application
- User authentication system
- Full CRUD for posts (owner-only edit/delete)
- Comment system with moderation
- Tag-based filtering
- Responsive design

**Concepts to Implement:**
- All concepts from I01-I19
- Complete CRUD pattern
- Permission-based access
- User-generated content

---

# 🟠 ADVANCED LEVEL (A01-A18)

*Focus: REST APIs, Django REST Framework, testing, middleware, custom commands, and caching*

---

## A01: Django REST Framework Setup ⭐⭐

**Learning Objectives:**
- Install and configure Django REST Framework
- Create basic API views
- Understand serialization fundamentals

**Requirements:**
1. Install djangorestframework
2. Add to INSTALLED_APPS
3. Configure REST_FRAMEWORK settings
4. Create simple API endpoint returning JSON
5. Test with browser and curl

**Deliverables:**
- DRF installed and configured
- Settings with authentication defaults
- Basic API endpoint working
- API tested with multiple methods

**Concepts to Implement:**
- DRF installation
- `REST_FRAMEWORK` settings
- `@api_view` decorator
- Response object

---

## A02: DRF Serializers ⭐⭐⭐

**Learning Objectives:**
- Create serializers for models
- Understand serialization/deserialization
- Validate data with serializers

**Requirements:**
1. Create `BlogPostSerializer` with all fields
2. Create `AuthorSerializer` with nested relations
3. Use `read_only` and `write_only` fields
4. Add custom validation methods
5. Test serializers in Django shell

**Deliverables:**
- Serializers for all models
- Nested serializer relationships
- Validation logic in serializers
- Shell demonstrations

**Concepts to Implement:**
- `serializers.ModelSerializer`
- `Meta` class configuration
- `SerializerMethodField`
- `validate_<field>()` methods

---

## A03: DRF Views and ViewSets ⭐⭐⭐

**Learning Objectives:**
- Use APIView for REST endpoints
- Implement ViewSets for CRUD
- Understand action routing

**Requirements:**
1. Create `BlogPostViewSet` with all CRUD operations
2. Create `AuthorViewSet` (read-only)
3. Add custom actions with `@action` decorator
4. Create API for tags
5. Document all endpoints

**Deliverables:**
- ViewSets for all models
- Custom actions (publish, unpublish)
- Complete CRUD APIs
- API documentation

**Concepts to Implement:**
- `ModelViewSet`, `ReadOnlyModelViewSet`
- `@action` decorator
- HTTP method to viewset method mapping
- Queryset filtering

---

## A04: DRF Routers and URLs ⭐⭐

**Learning Objectives:**
- Use routers for automatic URL generation
- Nest routers for hierarchical APIs
- Customize router behavior

**Requirements:**
1. Create `DefaultRouter` for viewsets
2. Register all viewsets with router
3. Add custom URL patterns alongside router
4. Implement versioned API URLs (v1)
5. Create API root with links

**Deliverables:**
- Router configuration
- Complete API URL structure
- Versioned API paths
- API root endpoint

**Concepts to Implement:**
- `DefaultRouter`, `SimpleRouter`
- `router.register()`
- URL namespacing
- API versioning

---

## A05: DRF Authentication ⭐⭐⭐

**Learning Objectives:**
- Implement multiple authentication methods
- Use token authentication
- Configure per-view authentication

**Requirements:**
1. Enable SessionAuthentication for browser
2. Implement TokenAuthentication
3. Create token obtain endpoint
4. Configure authentication per viewset
5. Test authenticated endpoints

**Deliverables:**
- Multiple auth methods configured
- Token authentication working
- Token endpoints for obtain/refresh
- Protected API endpoints

**Concepts to Implement:**
- `SessionAuthentication`, `TokenAuthentication`
- `authentication_classes`
- Token models
- `obtain_auth_token` view

---

## A06: DRF Permissions ⭐⭐⭐

**Learning Objectives:**
- Use built-in permission classes
- Create custom permissions
- Apply object-level permissions

**Requirements:**
1. Use `IsAuthenticated`, `IsAdminUser`
2. Create `IsOwnerOrReadOnly` permission
3. Apply permissions at view and object level
4. Create `IsPublishedOrOwner` for posts
5. Document permission logic

**Deliverables:**
- Permission classes in `permissions.py`
- Views with multiple permissions
- Object-level permission checks
- Permission documentation

**Concepts to Implement:**
- `permission_classes`
- `BasePermission` subclassing
- `has_permission()`, `has_object_permission()`
- Default permissions

---

## A07: DRF Filtering, Search, and Ordering ⭐⭐

**Learning Objectives:**
- Add filtering to API views
- Implement search functionality
- Enable ordering options

**Requirements:**
1. Install django-filter
2. Add `FilterSet` for BlogPost
3. Enable search on title and content
4. Enable ordering by date, title
5. Create filterable tag endpoint

**Deliverables:**
- Filter backend configured
- Custom FilterSet class
- Search functionality
- Ordering options

**Concepts to Implement:**
- `DjangoFilterBackend`
- `SearchFilter`, `OrderingFilter`
- `FilterSet` class
- `filterset_fields`, `search_fields`

---

## A08: DRF Pagination ⭐⭐

**Learning Objectives:**
- Configure API pagination
- Implement multiple pagination styles
- Customize pagination response

**Requirements:**
1. Enable global pagination
2. Create custom pagination class
3. Implement cursor pagination for large datasets
4. Add page size query parameter
5. Document pagination patterns

**Deliverables:**
- Pagination globally configured
- Custom pagination class
- Multiple pagination options
- API pagination documentation

**Concepts to Implement:**
- `PageNumberPagination`
- `LimitOffsetPagination`
- `CursorPagination`
- `pagination_class`

---

## A09: Unit Testing Models ⭐⭐⭐

**Learning Objectives:**
- Write unit tests for Django models
- Use setUp and tearDown
- Test model methods and properties

**Requirements:**
1. Create `test_models.py` with TestCase
2. Test model creation and saving
3. Test model `__str__` method
4. Test custom model methods
5. Test model validation

**Deliverables:**
- Test file with model tests
- Coverage for all model methods
- Passing test suite
- Test documentation

**Concepts to Implement:**
- `django.test.TestCase`
- `setUp()`, `tearDown()`
- Model assertions
- `assertRaises` for validation

---

## A10: Unit Testing Views ⭐⭐⭐

**Learning Objectives:**
- Test views with Django's test client
- Test authenticated endpoints
- Mock external dependencies

**Requirements:**
1. Create `test_views.py`
2. Test GET and POST requests
3. Test authenticated views
4. Test view with different users
5. Test redirects and error responses

**Deliverables:**
- View tests with test client
- Authentication testing
- Response assertion patterns
- Complete view coverage

**Concepts to Implement:**
- `Client` for testing
- `self.client.login()`
- `response.status_code` assertions
- `response.context` testing

---

## A11: Testing Django REST Framework ⭐⭐⭐

**Learning Objectives:**
- Use DRF's test utilities
- Test API endpoints comprehensively
- Test with authentication tokens

**Requirements:**
1. Use `APITestCase` and `APIClient`
2. Test all CRUD operations
3. Test with authenticated user
4. Test permission restrictions
5. Test validation errors

**Deliverables:**
- `test_api.py` with API tests
- All endpoints tested
- Permission testing
- Validation error testing

**Concepts to Implement:**
- `APITestCase`, `APIClient`
- `force_authenticate()`
- API response assertions
- Status code verification

---

## A12: Integration Testing ⭐⭐⭐

**Learning Objectives:**
- Write integration tests
- Test complete user workflows
- Use factory patterns for test data

**Requirements:**
1. Install and use factory_boy
2. Create factories for all models
3. Write workflow tests (register → create post → comment)
4. Test email sending (mock)
5. Test file uploads

**Deliverables:**
- Factory classes for all models
- Integration test workflows
- Mocked external services
- File upload testing

**Concepts to Implement:**
- `factory_boy` factories
- Workflow testing
- `mock.patch()` for mocking
- `SimpleUploadedFile`

---

## A13: Custom Django Middleware ⭐⭐⭐

**Learning Objectives:**
- Understand middleware architecture
- Create custom middleware
- Process requests and responses

**Requirements:**
1. Create logging middleware (request timing)
2. Create maintenance mode middleware
3. Create user timezone middleware
4. Add middleware to MIDDLEWARE setting
5. Test middleware functionality

**Deliverables:**
- `middleware.py` with custom middleware
- Request/response processing
- Middleware order documentation
- Working middleware tests

**Concepts to Implement:**
- Middleware class structure
- `__init__`, `__call__` methods
- `process_request`, `process_response`
- Middleware ordering

---

## A14: Custom Management Commands ⭐⭐⭐

**Learning Objectives:**
- Create custom Django commands
- Handle command arguments
- Schedule commands with cron

**Requirements:**
1. Create `populate_sample_data` command
2. Create `delete_old_drafts` command
3. Create `send_weekly_digest` command
4. Add command arguments and options
5. Add progress output and error handling

**Deliverables:**
- Commands in `management/commands/`
- Working commands with arguments
- Error handling and logging
- Documentation for each command

**Concepts to Implement:**
- `BaseCommand` subclassing
- `add_arguments()` method
- `handle()` method
- `self.stdout.write()`

---

## A15: Signals Deep Dive ⭐⭐⭐

**Learning Objectives:**
- Use Django signals effectively
- Create custom signals
- Avoid common signal pitfalls

**Requirements:**
1. Use `pre_save` to validate data
2. Use `post_save` for notifications
3. Use `post_delete` for cleanup
4. Create custom signal for publishing
5. Document signal best practices

**Deliverables:**
- `signals.py` with signal handlers
- Connected signals in `apps.py`
- Custom signal implementation
- Signal documentation

**Concepts to Implement:**
- `@receiver` decorator
- `post_save`, `pre_save`, `post_delete`
- `dispatch_uid` for uniqueness
- Custom signal creation

---

## A16: Caching Strategies ⭐⭐⭐

**Learning Objectives:**
- Configure Django caching
- Implement view and template caching
- Use cache API for manual caching

**Requirements:**
1. Configure Redis cache backend
2. Implement per-view caching
3. Use `{% cache %}` template tag
4. Manual cache API usage
5. Cache invalidation strategies

**Deliverables:**
- Cache configuration (Redis)
- Cached views
- Template fragment caching
- Cache invalidation logic

**Concepts to Implement:**
- `CACHES` configuration
- `@cache_page` decorator
- `{% cache time key %}`
- `cache.set()`, `cache.get()`

---

## A17: Database Optimization ⭐⭐⭐

**Learning Objectives:**
- Identify N+1 query problems
- Use select_related and prefetch_related
- Optimize database queries

**Requirements:**
1. Install django-debug-toolbar
2. Identify N+1 queries in existing views
3. Fix with `select_related` for ForeignKey
4. Fix with `prefetch_related` for ManyToMany
5. Use `only()` and `defer()` for partial loading

**Deliverables:**
- Debug toolbar configured
- Optimized views with no N+1
- Query count before/after comparison
- Performance documentation

**Concepts to Implement:**
- `select_related()`, `prefetch_related()`
- `Prefetch` object for custom querysets
- `only()`, `defer()`
- Query analysis

---

## A18: Advanced Capstone - REST API for Blog ⭐⭐⭐⭐

**Learning Objectives:**
- Build a complete REST API
- Implement comprehensive testing
- Apply optimization and caching

**Requirements:**
1. Complete REST API with:
   - Full CRUD for posts, comments, tags
   - Token authentication
   - Permissions (owner-based)
   - Filtering, search, ordering
   - Pagination
2. Test suite with >80% coverage
3. Custom middleware and commands
4. Caching for expensive endpoints
5. API documentation (Swagger/OpenAPI)

**Deliverables:**
- Complete REST API
- Comprehensive test suite
- Swagger documentation
- Performance optimizations
- Custom middleware and commands
- README with API documentation

**Concepts to Implement:**
- All concepts from A01-A17
- API best practices
- Testing patterns
- Performance optimization

---

# 🔴 EXPERT LEVEL (E01-E14)

*Focus: Security, performance, deployment, and production patterns*

---

## E01: Security Hardening ⭐⭐⭐

**Learning Objectives:**
- Implement Django security best practices
- Configure security middleware
- Protect against common vulnerabilities

**Requirements:**
1. Enable all security middleware
2. Configure CSRF protection properly
3. Set up Content Security Policy
4. Enable HSTS and secure cookies
5. Audit with `./manage.py check --deploy`

**Deliverables:**
- Security settings configured
- CSP headers implemented
- Security audit passing
- Security documentation

**Concepts to Implement:**
- `SecurityMiddleware` settings
- `CSRF_COOKIE_SECURE`, `SESSION_COOKIE_SECURE`
- CSP headers
- Security checklist

---

## E02: Rate Limiting and Throttling ⭐⭐⭐

**Learning Objectives:**
- Implement API rate limiting
- Configure DRF throttling
- Create custom throttle classes

**Requirements:**
1. Configure default throttle rates
2. Create `UserRateThrottle` for authenticated
3. Create `AnonRateThrottle` for anonymous
4. Create custom throttle for specific endpoints
5. Return proper rate limit headers

**Deliverables:**
- Throttling configured globally
- Custom throttle classes
- Per-endpoint throttling
- Rate limit response headers

**Concepts to Implement:**
- `DEFAULT_THROTTLE_CLASSES`
- `UserRateThrottle`, `AnonRateThrottle`
- Custom throttle classes
- Throttle scope

---

## E03: Async Views and Performance ⭐⭐⭐⭐

**Learning Objectives:**
- Implement async views
- Use async database queries
- Configure ASGI for async support

**Requirements:**
1. Convert sync views to async
2. Use `sync_to_async` for ORM
3. Implement async external API calls
4. Configure ASGI server (uvicorn/daphne)
5. Benchmark sync vs async performance

**Deliverables:**
- Async views implemented
- ASGI server configuration
- Performance benchmarks
- Async patterns documentation

**Concepts to Implement:**
- `async def` views
- `sync_to_async`
- ASGI configuration
- `httpx` for async HTTP

---

## E04: Background Tasks with Celery ⭐⭐⭐⭐

**Learning Objectives:**
- Set up Celery with Django
- Create and execute async tasks
- Monitor task execution

**Requirements:**
1. Install and configure Celery with Redis
2. Create tasks for email sending
3. Create scheduled tasks (beat)
4. Implement task retry logic
5. Set up Flower for monitoring

**Deliverables:**
- Celery configuration
- Background task implementations
- Scheduled tasks with beat
- Flower monitoring setup

**Concepts to Implement:**
- `celery.py` configuration
- `@shared_task` decorator
- Celery beat scheduler
- Task monitoring

---

## E05: File Uploads and Media Handling ⭐⭐⭐

**Learning Objectives:**
- Handle file uploads securely
- Validate file types and sizes
- Configure cloud storage

**Requirements:**
1. Implement secure file upload view
2. Validate file types and sizes
3. Generate thumbnails for images
4. Configure S3 storage backend
5. Implement signed URLs for private files

**Deliverables:**
- Secure file upload handling
- File validation logic
- S3 storage configuration
- Signed URL generation

**Concepts to Implement:**
- `FileField`, `ImageField` handling
- `django-storages` for S3
- File validation
- Signed URL generation

---

## E06: Email Configuration and Templates ⭐⭐⭐

**Learning Objectives:**
- Configure email backends
- Create HTML email templates
- Send transactional emails

**Requirements:**
1. Configure SMTP backend
2. Create HTML email templates
3. Implement welcome email on registration
4. Implement password reset emails
5. Use email templating library

**Deliverables:**
- Email configuration
- HTML email templates
- Transactional email sending
- Email testing setup

**Concepts to Implement:**
- `EMAIL_BACKEND` configuration
- `send_mail()`, `EmailMessage`
- HTML email templating
- Email preview/testing

---

## E07: Multi-tenancy Patterns ⭐⭐⭐⭐

**Learning Objectives:**
- Implement schema-based multi-tenancy
- Configure tenant routing
- Handle tenant-specific data

**Requirements:**
1. Implement tenant model
2. Create tenant middleware
3. Filter querysets by tenant
4. Handle tenant switching
5. Configure tenant-specific settings

**Deliverables:**
- Tenant model and middleware
- Tenant-aware querysets
- Tenant switching logic
- Multi-tenant documentation

**Concepts to Implement:**
- Tenant identification
- Middleware for tenant context
- QuerySet filtering
- Shared vs tenant-specific models

---

## E08: API Versioning Strategies ⭐⭐⭐

**Learning Objectives:**
- Implement API versioning
- Handle breaking changes
- Maintain backward compatibility

**Requirements:**
1. Implement URL-based versioning
2. Implement header-based versioning
3. Create v1 and v2 serializers
4. Handle deprecated endpoints
5. Document versioning strategy

**Deliverables:**
- Multiple API versions
- Version routing logic
- Deprecation handling
- Versioning documentation

**Concepts to Implement:**
- `AcceptHeaderVersioning`
- `URLPathVersioning`
- Version-specific serializers
- Deprecation warnings

---

## E09: WebSockets with Django Channels ⭐⭐⭐⭐

**Learning Objectives:**
- Set up Django Channels
- Implement WebSocket consumers
- Create real-time features

**Requirements:**
1. Install and configure Channels
2. Create chat room consumer
3. Implement real-time notifications
4. Configure channel layers (Redis)
5. Create frontend WebSocket client

**Deliverables:**
- Channels configuration
- WebSocket consumer
- Real-time chat feature
- Notification system

**Concepts to Implement:**
- `channels` configuration
- WebSocket consumers
- Channel layers
- ASGI routing

---

## E10: Logging and Monitoring ⭐⭐⭐

**Learning Objectives:**
- Configure comprehensive logging
- Implement structured logging
- Set up error monitoring

**Requirements:**
1. Configure logging to file and console
2. Create custom formatters
3. Integrate with Sentry for errors
4. Add request ID logging
5. Create log analysis patterns

**Deliverables:**
- Logging configuration
- Custom log handlers
- Sentry integration
- Log analysis documentation

**Concepts to Implement:**
- `LOGGING` configuration
- Custom handlers and formatters
- Sentry SDK
- Correlation IDs

---

## E11: Docker Configuration ⭐⭐⭐

**Learning Objectives:**
- Containerize Django application
- Create multi-stage Dockerfile
- Configure docker-compose for development

**Requirements:**
1. Create optimized Dockerfile
2. Create docker-compose.yml with services
3. Configure for PostgreSQL and Redis
4. Set up volume for development
5. Create production docker-compose

**Deliverables:**
- Optimized Dockerfile
- Development docker-compose
- Production docker-compose
- Container documentation

**Concepts to Implement:**
- Multi-stage builds
- Docker networking
- Volume configuration
- Environment management

---

## E12: CI/CD Pipeline ⭐⭐⭐⭐

**Learning Objectives:**
- Set up continuous integration
- Configure automated testing
- Implement deployment pipeline

**Requirements:**
1. Create GitHub Actions workflow
2. Run tests on push
3. Check code coverage
4. Build Docker image on main
5. Deploy to staging automatically

**Deliverables:**
- CI workflow configuration
- Test and coverage steps
- Docker build automation
- Staging deployment

**Concepts to Implement:**
- GitHub Actions
- Test automation
- Docker builds
- Deployment triggers

---

## E13: Production Deployment ⭐⭐⭐⭐

**Learning Objectives:**
- Deploy Django to production
- Configure reverse proxy
- Set up SSL/TLS

**Requirements:**
1. Configure Gunicorn with workers
2. Set up Nginx as reverse proxy
3. Configure SSL with Let's Encrypt
4. Set up proper environment variables
5. Configure database backups

**Deliverables:**
- Gunicorn configuration
- Nginx configuration
- SSL setup
- Backup strategy

**Concepts to Implement:**
- WSGI server configuration
- Reverse proxy setup
- SSL/TLS termination
- Production settings

---

## E14: Expert Capstone - Production SaaS Application ⭐⭐⭐⭐

**Learning Objectives:**
- Build a production-ready SaaS application
- Implement all security best practices
- Deploy with full production infrastructure

**Requirements:**
1. Complete SaaS application with:
   - Multi-tenant architecture
   - Subscription billing integration
   - Admin dashboard
   - API with documentation
   - Real-time features
2. Full test coverage (>85%)
3. Docker deployment
4. CI/CD pipeline
5. Monitoring and logging
6. Documentation

**Deliverables:**
- Production-ready SaaS application
- Complete API with Swagger docs
- Multi-tenant implementation
- CI/CD configuration
- Monitoring dashboards
- Production deployment guide
- Comprehensive documentation

**Concepts to Implement:**
- All concepts from E01-E13
- Production patterns
- SaaS architecture
- Full-stack deployment

---

# 📚 Appendix

## Recommended Project Structure

```
myproject/
├── config/                 # Project configuration
│   ├── settings/
│   │   ├── base.py
│   │   ├── development.py
│   │   └── production.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── apps/                   # Django applications
│   ├── accounts/
│   ├── blog/
│   └── api/
├── templates/              # Project-level templates
├── static/                 # Project-level static files
├── media/                  # User-uploaded files
├── tests/                  # Test files
├── requirements/
│   ├── base.txt
│   ├── development.txt
│   └── production.txt
├── docker/
├── .github/workflows/
├── manage.py
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## Difficulty Progression Chart

```
Level      Assignments    Cumulative Concepts
─────────────────────────────────────────────
Beginner   18 (B01-B18)   ~20 core concepts
Intermediate 20 (I01-I20)  ~45 concepts
Advanced   18 (A01-A18)   ~70 concepts
Expert     14 (E01-E14)   ~90 concepts (production-ready)
```

## Prerequisites Checklist

- [ ] Python 3.10+ installed
- [ ] Basic Python knowledge (functions, classes, modules)
- [ ] Understanding of HTTP and REST basics
- [ ] Familiarity with command line
- [ ] Git version control basics
- [ ] Text editor or IDE (VS Code recommended)

## Estimated Completion Time

| Level | Time Investment |
|-------|----------------|
| Beginner | 25-35 hours |
| Intermediate | 40-55 hours |
| Advanced | 50-70 hours |
| Expert | 60-80 hours |
| **Total** | **175-240 hours** |

---

> **🎓 Completion Milestone**: Upon completing all 70 assignments, you will have the skills to build, test, and deploy production-grade Django applications following industry best practices.
