# Chapter 20: Web Frameworks

> **Topics Covered**: WSGI, Flask basics, routes, templates, request/response, Django overview, REST APIs, FastAPI basics, middleware, forms, sessions, authentication, deployment concepts

---

## Questions

---

**Q20.1: Basic - [What is WSGI]**

What is WSGI?

A) Web framework
B) Web Server Gateway Interface — standard Python web server/application communication
C) Web security
D) Database protocol

**Answer: B**

**Explanation:**
WSGI (PEP 3333): standardizes how web servers (Gunicorn, uWSGI) communicate with Python web applications (Flask, Django). Callable takes environ, start_response. Foundation for Python web.

---

**Q20.2: Basic - [Flask Hello World]**

What is the output when visiting http://localhost:5000/?
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

A) Flask app
B) `Hello, World!` in browser
C) Error
D) Empty page

**Answer: B**

**Explanation:**
Flask: micro-framework for web apps. `@app.route('/')` maps URL to function. Function returns response body. `app.run()` starts development server. Simple, explicit structure.

---

**Q20.3: Intermediate - [Route Parameters]**

What is the output for `/user/42`?
```python
@app.route('/user/<int:user_id>')
def user(user_id):
    return f'User {user_id}'
```

A) `User <int:user_id>`
B) `User 42`
C) Error
D) `User None`

**Answer: B**

**Explanation:**
`<int:user_id>` captures URL segment as integer. Also: `<string:name>`, `<path:file>`, `<uuid:id>`. Converters validate and convert. Invalid format returns 404.

---

**Q20.4: Intermediate - [HTTP Methods]**

What does this allow?
```python
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        # handle form
    return render_template('login.html')
```

A) Only GET
B) Both GET and POST requests to /login
C) Any method
D) Error

**Answer: B**

**Explanation:**
`methods=` specifies allowed HTTP methods. GET for showing form, POST for submitting. Check `request.method` to handle differently. Default is GET only.

---

**Q20.5: Intermediate - [Request Object]**

What does `request.args` contain in Flask?

A) Command line arguments
B) Query string parameters (URL ?key=value)
C) POST form data
D) HTTP headers

**Answer: B**

**Explanation:**
`request.args` = query params (`?name=Alice`). `request.form` = form POST data. `request.json` = JSON body. `request.headers` = HTTP headers. `request.files` = uploaded files.

---

**Q20.6: Intermediate - [Templates]**

What is the output?
```python
# Template: hello.html
# <h1>Hello, {{ name }}!</h1>

@app.route('/hello/<name>')
def hello(name):
    return render_template('hello.html', name=name)
```

A) `{{ name }}`
B) `Hello, Alice!` (for /hello/Alice)
C) Template source
D) Error

**Answer: B**

**Explanation:**
Jinja2 templates: `{{ var }}` for variables, `{% for %}` for logic. `render_template` finds template in `templates/` folder, fills in variables. Separation of concerns.

---

**Q20.7: Intermediate - [Template Inheritance]**

What is template inheritance in Jinja2?

A) Python inheritance
B) Base template defines blocks, child templates override blocks
C) CSS inheritance
D) Variable sharing

**Answer: B**

**Explanation:**
Base: `{% block content %}{% endblock %}`. Child: `{% extends "base.html" %}{% block content %}...{% endblock %}`. Common layout (header, footer) in base, pages override content. DRY templates.

---

**Q20.8: Intermediate - [Flask Response]**

What is the output?
```python
from flask import jsonify

@app.route('/api/data')
def api_data():
    return jsonify({'status': 'ok', 'count': 10})
```

A) String `{'status': 'ok'}`
B) JSON response with Content-Type application/json
C) Dict object
D) Error

**Answer: B**

**Explanation:**
`jsonify()` returns Response with JSON body and proper Content-Type. For REST APIs. Can also: `return {'key': 'value'}` (Flask 1.0+ auto-jsonifies dicts).

---

**Q20.9: Intermediate - [Error Handling]**

What does this do?
```python
@app.errorhandler(404)
def not_found(error):
    return render_template('404.html'), 404
```

A) Raises 404
B) Custom 404 error page handler
C) Catches all errors
D) Logging

**Answer: B**

**Explanation:**
`@errorhandler(code)` customizes error responses. Returns tuple (response, status_code). Can also handle exception classes. User-friendly error pages instead of default.

---

**Q20.10: Intermediate - [Flask Blueprints]**

What are Flask Blueprints?

A) Documentation
B) Way to organize routes into modules/packages for large apps
C) Templates
D) Middleware

**Answer: B**

**Explanation:**
`bp = Blueprint('auth', __name__)`. Define routes on blueprint: `@bp.route('/login')`. Register: `app.register_blueprint(bp, url_prefix='/auth')`. Modular application structure.

---

**Q20.11: Intermediate - [Flask Sessions]**

What is the output?
```python
from flask import session

@app.route('/set')
def set_session():
    session['user'] = 'Alice'
    return 'Set'

@app.route('/get')
def get_session():
    return session.get('user', 'Anonymous')
```

A) Always 'Anonymous'
B) 'Alice' after visiting /set, persists across requests
C) Error
D) 'Set'

**Answer: B**

**Explanation:**
Flask session: client-side cookie (signed, not encrypted). Data persists per user. Requires `app.secret_key`. Server-side sessions with Flask-Session extension. Stateful web apps.

---

**Q20.12: Basic - [Django Overview]**

What is Django's philosophy?

A) Micro-framework
B) "Batteries included" — full-featured framework with ORM, admin, auth built-in
C) Minimal core
D) Template-only

**Answer: B**

**Explanation:**
Django: high-level web framework. Includes: ORM, admin interface, authentication, forms, templating. "Don't repeat yourself." MTV (Model-Template-View) pattern. Rapid development for complex apps.

---

**Q20.13: Intermediate - [Django vs Flask]**

When choose Flask over Django?

A) Always Flask
B) Small apps, APIs, microservices where you choose components; Django for full-featured apps
C) Never Flask
D) Performance only

**Answer: B**

**Explanation:**
Flask: freedom to choose components, learning curve, small projects, APIs. Django: all-in-one, rapid development, standard patterns, larger projects. Both excellent — depends on needs.

---

**Q20.14: Intermediate - [Django URL Patterns]**

What does this Django URL pattern do?
```python
# urls.py
path('article/<int:year>/', views.year_archive)
```

A) Static URL
B) Captures year as integer, passes to year_archive view
C) Creates year
D) Error

**Answer: B**

**Explanation:**
Django URL converters like Flask. `<int:year>` captures integer. View receives: `def year_archive(request, year):`. Pattern matching from URLconf. `re_path()` for regex patterns.

---

**Q20.15: Intermediate - [Django ORM]**

What is the output (conceptually)?
```python
# models.py
class Article(models.Model):
    title = models.CharField(max_length=200)

# views.py
articles = Article.objects.filter(title__contains='Python')
```

A) SQL string
B) QuerySet of articles with "Python" in title
C) List of strings
D) Error

**Answer: B**

**Explanation:**
Django ORM: `objects.filter()` returns QuerySet (lazy). `__contains` is lookup. Translated to SQL LIKE. Also: `__exact`, `__gt`, `__startswith`. QuerySets are chainable, lazy-evaluated.

---

**Q20.16: Intermediate - [Django Admin]**

What does Django admin provide?

A) CLI tool
B) Auto-generated CRUD interface for models
C) Server management
D) Code generator

**Answer: B**

**Explanation:**
`admin.site.register(Model)` — instant web interface for data management. Create, read, update, delete without coding. Customizable. Huge time saver for internal tools, prototyping.

---

**Q20.17: Basic - [FastAPI Overview]**

What makes FastAPI special?

A) Fastest Python
B) Automatic OpenAPI docs, type hints for validation, async support, high performance
C) AI integration
D) Only for APIs

**Answer: B**

**Explanation:**
FastAPI: modern, type hints for validation and docs. Auto-generates OpenAPI (Swagger) UI. Async-native. Uses Pydantic for validation. Starlette underneath. Comparable speed to Node.js/Go.

---

**Q20.18: Intermediate - [FastAPI Type Validation]**

What is the output for `/items/abc`?
```python
from fastapi import FastAPI
app = FastAPI()

@app.get('/items/{item_id}')
def read_item(item_id: int):
    return {'item_id': item_id}
```

A) `{'item_id': 'abc'}`
B) 422 Validation Error — "abc" is not a valid integer
C) Error 500
D) `{'item_id': 0}`

**Answer: B**

**Explanation:**
Type hints enforced! `item_id: int` validates input. Invalid type → 422 with detailed error. Pydantic validates. Built-in data validation without manual code.

---

**Q20.19: Intermediate - [Pydantic Models]**

What does this do?
```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = False

@app.post('/items/')
def create_item(item: Item):
    return item
```

A) Dictionary input
B) Validates JSON body matches Item schema, rejects invalid data
C) No validation
D) Only name required

**Answer: B**

**Explanation:**
Pydantic BaseModel in FastAPI: request body validation. Must have name (str), price (float). `is_offer` optional with default. Invalid types → 422. Automatic, documented API contract.

---

**Q20.20: Intermediate - [FastAPI Docs]**

What URLs does FastAPI auto-generate?

A) None
B) `/docs` (Swagger UI), `/redoc` (ReDoc) — interactive API documentation
C) `/api` only
D) Must configure manually

**Answer: B**

**Explanation:**
FastAPI generates OpenAPI spec from type hints. `/docs` = Swagger UI (interactive). `/redoc` = alternative docs. Test endpoints directly from browser. Documentation as code — always in sync.

---

**Q20.21: Intermediate - [Middleware]**

What is web middleware?

A) Hardware
B) Code that runs before/after each request — logging, auth, CORS, etc.
C) Database layer
D) Template engine

**Answer: B**

**Explanation:**
Middleware wraps request handling. Flask: `@app.before_request`. Django: MIDDLEWARE setting. FastAPI: `@app.middleware("http")`. Common uses: logging, authentication, CORS headers, compression.

---

**Q20.22: Intermediate - [CORS Middleware]**

What is CORS middleware for?

A) Security
B) Enables cross-origin requests from browsers (different domain)
C) Compression
D) Caching

**Answer: B**

**Explanation:**
Browsers block cross-origin requests by default. CORS middleware adds `Access-Control-Allow-Origin` header. Required for JavaScript frontend calling API on different domain.

---

**Q20.23: Intermediate - [REST API Design]**

What's a RESTful endpoint for getting all users?

A) `POST /getUsers`
B) `GET /users`
C) `GET /user/all`
D) `FETCH /users`

**Answer: B**

**Explanation:**
REST: resources as nouns, HTTP methods as verbs. `/users` (plural) for collection. `GET /users` = list, `POST /users` = create, `GET /users/1` = one user, `PUT /users/1` = update.

---

**Q20.24: Intermediate - [API Versioning]**

How to version REST APIs?

A) No versioning needed
B) URL path (`/v1/users`), header (`Accept-Version`), or query param
C) Different servers
D) Database version

**Answer: B**

**Explanation:**
Breaking changes need versioning. URL path most common: `/api/v1/...`. Header versioning (content negotiation) cleaner but complex. Plan for version 2 from start.

---

**Q20.25: Intermediate - [Request Validation]**

Why validate API input?

A) Optional
B) Security (injection), data integrity, meaningful errors
C) Performance
D) Only for forms

**Answer: B**

**Explanation:**
Never trust client input. Validate: types, ranges, formats, required fields. Prevents: SQL injection, XSS, data corruption. Return 400/422 with details. Pydantic, marshmallow, WTForms for Python.

---

**Q20.26: Intermediate - [Form Handling]**

What does WTForms provide in Flask?

A) HTML templates
B) Form classes with validation, CSRF protection, rendering
C) Database forms
D) JavaScript forms

**Answer: B**

**Explanation:**
```python
class LoginForm(FlaskForm):
    username = StringField(validators=[DataRequired()])
```
Validates on submit. CSRF token automatic. Render in template. Flask-WTF integrates with Flask.

---

**Q20.27: Intermediate - [CSRF Protection]**

What is CSRF?

A) CSS framework
B) Cross-Site Request Forgery — attacker tricks browser into making authenticated request
C) Caching
D) Session storage

**Answer: B**

**Explanation:**
CSRF: logged-in user visits malicious site, which submits request to your app. Browser sends cookies automatically. Protection: unique token per form, verify on submit. Most frameworks include CSRF protection.

---

**Q20.28: Intermediate - [Authentication Methods]**

Common web authentication methods:

A) Only passwords
B) Session cookies, JWT tokens, OAuth, API keys
C) Database auth
D) IP-based

**Answer: B**

**Explanation:**
Sessions: server stores state, cookie references it. JWT: self-contained token, stateless. OAuth: delegated auth (Login with Google). API keys: simple, for machine clients. Choose based on use case.

---

**Q20.29: Intermediate - [Password Hashing]**

Why hash passwords?

A) Encryption
B) If database leaked, attackers can't get actual passwords (if properly hashed)
C) Faster comparison
D) Required by law

**Answer: B**

**Explanation:**
Hash = one-way function. Store hash, not password. On login: hash input, compare hashes. If DB stolen, passwords aren't exposed. Use bcrypt, argon2 — NOT MD5/SHA1 alone.

---

**Q20.30: Intermediate - [Flask-Login]**

What does Flask-Login provide?

A) Login page
B) Session management for logged-in users (login, logout, remember me)
C) OAuth only
D) Password storage

**Answer: B**

**Explanation:**
Flask-Login: `@login_required` decorator, `current_user` proxy, login/logout helpers, remember me. You implement user loading and password verification. Common Flask auth extension.

---

**Q20.31: Intermediate - [Dependency Injection]**

What is dependency injection in FastAPI?
```python
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.get('/users/')
def read_users(db: Session = Depends(get_db)):
    ...
```

A) Database creation
B) Framework injects dependencies (db) into endpoint functions
C) Import injection
D) Variable passing

**Answer: B**

**Explanation:**
`Depends()` declares dependencies. FastAPI calls `get_db()`, passes result to function, handles cleanup. Clean, testable code. Can chain dependencies. Similar to pytest fixtures.

---

**Q20.32: Intermediate - [Static Files]**

How do Flask/FastAPI serve static files?

A) No static support
B) `static/` folder, served at `/static/` URL (development only — use CDN/nginx in production)
C) Template embedding
D) Database storage

**Answer: B**

**Explanation:**
Development: `app.static_folder = 'static'`. Access: `/static/style.css`. Production: serve via nginx, CDN for performance. Never serve static files through Python in production.

---

**Q20.33: Intermediate - [Async Endpoints]**

What is the output?
```python
@app.get('/async')
async def async_endpoint():
    await asyncio.sleep(1)
    return {'status': 'done'}
```

A) Error
B) Returns after 1 second, non-blocking for other requests
C) Same as sync
D) Immediate return

**Answer: B**

**Explanation:**
FastAPI (Starlette) and async Flask support `async def` endpoints. During `await`, other requests can be handled. Non-blocking I/O. Use for I/O-bound operations (database, HTTP calls).

---

**Q20.34: Intermediate - [Deployment Options]**

Common Python web app deployment:

A) `python app.py`
B) Gunicorn/uWSGI + nginx, containerized with Docker, cloud platforms
C) Apache only
D) Development server

**Answer: B**

**Explanation:**
Production: WSGI server (Gunicorn, uWSGI) for multi-process. nginx as reverse proxy (static files, SSL, load balancing). Docker for containerization. Platforms: Heroku, AWS, GCP, Railway.

---

**Q20.35: Intermediate - [Gunicorn]**

What does `gunicorn -w 4 app:app` do?

A) Compiles app
B) Runs WSGI app with 4 worker processes
C) Creates 4 apps
D) Testing

**Answer: B**

**Explanation:**
Gunicorn: production WSGI server. `-w 4` = 4 worker processes (utilize multiple cores). `app:app` = module:variable (Flask/Django app). Production-ready, unlike development servers.

---

**Q20.36: Intermediate - [Environment Variables]**

Why use environment variables for config?

A) Faster
B) Keeps secrets out of code, different values per environment
C) Required
D) Logging

**Answer: B**

**Explanation:**
`os.environ['DATABASE_URL']`. Never commit secrets to git. Different values: development, staging, production. 12-factor app principle. Use python-dotenv for .env files locally.

---

**Q20.37: Intermediate - [Health Check Endpoints]**

What is `/health` or `/readiness` endpoint for?

A) User health data
B) Let load balancers/orchestrators check if app is running properly
C) Documentation
D) Debugging

**Answer: B**

**Explanation:**
Kubernetes, load balancers call health endpoints. Return 200 if healthy. Check database connections, dependencies. Readiness: can accept traffic. Liveness: is it alive. System reliability.

---

**Q20.38: Intermediate - [Rate Limiting]**

Why implement rate limiting?

A) Slow down app
B) Prevent abuse, protect resources from excessive requests
C) Required by HTTP
D) Only for paid APIs

**Answer: B**

**Explanation:**
Rate limiting: max requests per time period per user/IP. Prevents: DDoS, brute force, scraping. Return 429 Too Many Requests. Libraries: Flask-Limiter, slowapi (FastAPI). Or use API gateway.

---

**Q20.39: Intermediate - [API Response Patterns]**

What's a good API response structure?
```python
{
    "success": true,
    "data": {...},
    "error": null
}
```

A) Any structure
B) Consistent structure with status, data, error for predictable client handling
C) Just data
D) XML only

**Answer: B**

**Explanation:**
Consistent responses: clients know what to expect. Include: success indicator, data payload, error details when applicable. Also: consistent error format with codes and messages. API contract.

---

**Q20.40: Intermediate - [Pagination]**

What's a good pagination response?
```python
{
    "items": [...],
    "total": 100,
    "page": 1,
    "per_page": 10,
    "next_page": 2
}
```

A) Return all items
B) Return page of items with metadata for navigation
C) No standard
D) Use offset only

**Answer: B**

**Explanation:**
Don't return thousands of items. Page-based or cursor-based pagination. Metadata helps clients navigate. `?page=2&per_page=50` or `?cursor=xyz`. Large datasets need pagination.

---

**Q20.41: Intermediate - [WebSocket Handling]**

How do Flask/FastAPI handle WebSockets?

A) Built-in full support
B) Flask-SocketIO for Flask; FastAPI has native WebSocket support
C) Not supported
D) Only HTTP

**Answer: B**

**Explanation:**
Flask: Flask-SocketIO extension (Socket.IO protocol). FastAPI: `@app.websocket("/ws")` built-in. WebSockets for real-time bidirectional communication. Different from REST request-response.

---

**Q20.42: Intermediate - [Database Connections]**

How to manage database connections in web apps?

A) One global connection
B) Connection pool — reuse connections, prevent exhaustion
C) New connection per request
D) Keep all connections open

**Answer: B**

**Explanation:**
Web apps handle concurrent requests. Connection pooling: maintain N open connections, reuse them. SQLAlchemy, Django manage pools. Prevent: connection exhaustion, overhead of creating connections.

---

**Q20.43: Intermediate - [Request Context]**

What is Flask's request context?

A) Request class
B) Thread-local storage for current request data (request, session, g)
C) Global request
D) Middleware

**Answer: B**

**Explanation:**
`request`, `session`, `g` are thread-local proxies. Each request has own context. Access anywhere without passing around. `g` for request-scoped storage. Convenient but understand scope.

---

**Q20.44: Intermediate - [Testing Web Apps]**

How to test Flask/FastAPI endpoints?

A) Manual browser testing only
B) Test client: `client.get('/'), client.post('/', json={...})`
C) Unit tests only
D) Production testing

**Answer: B**

**Explanation:**
Flask: `app.test_client()`. FastAPI: `TestClient(app)` from Starlette. Make requests, assert responses. No need to start server. Automated testing of API endpoints. pytest integration.

---

**Q20.45: Intermediate - [Serialization]**

What is API serialization?

A) Database storage
B) Converting Python objects to JSON/dict for API responses
C) Compression
D) Encryption

**Answer: B**

**Explanation:**
ORM objects have fields, relationships. Serialize to JSON for API. Control what fields to include, format dates, nest related objects. Pydantic, marshmallow, Django serializers handle this.

---

**Q20.46: Intermediate - [GraphQL Integration]**

How to add GraphQL to Python web apps?

A) Built-in
B) Libraries: Strawberry, Graphene, Ariadne
C) REST only
D) Different language

**Answer: B**

**Explanation:**
GraphQL: alternative to REST, client specifies exact data needed. Strawberry: modern, type-hints. Graphene: mature. Add to Flask/FastAPI/Django. Single endpoint, flexible queries.

---

**Q20.47: Intermediate - [Caching]**

Why cache API responses?

A) Use more memory
B) Reduce database load, faster responses for repeated requests
C) Required
D) Debug only

**Answer: B**

**Explanation:**
Cache expensive queries, external API calls. Flask-Caching, Redis. `@cache.cached(timeout=60)`. Also: HTTP caching headers (Cache-Control, ETag). Balance freshness vs performance.

---

**Q20.48: Intermediate - [Background Tasks]**

How to run long tasks without blocking requests?

A) Make user wait
B) Background task queue (Celery, RQ, FastAPI BackgroundTasks)
C) Faster server
D) Not possible

**Answer: B**

**Explanation:**
Send email, process file — don't make HTTP request wait. Queue task, return immediately. Celery + Redis/RabbitMQ for complex needs. FastAPI: `BackgroundTasks` for simple cases. Async processing.

---

**Q20.49: Intermediate - [Logging Best Practices]**

What should you log in web apps?

A) Everything
B) Requests, errors, important events; structured logging with request IDs
C) Nothing in production
D) Only errors

**Answer: B**

**Explanation:**
Log: incoming requests, response times, errors with tracebacks, security events. Structured logging (JSON) for parsing. Request ID for tracing. Log levels for filtering. ELK stack, cloud logging.

---

**Q20.50: Intermediate - [Production Checklist]**

What's important for production web apps?

A) Development settings work
B) Debug off, HTTPS, secrets from env, logging, monitoring, database pool, static via CDN
C) Single process
D) Print statements

**Answer: B**

**Explanation:**
Debug mode: off (security). Secrets: env vars, not code. HTTPS: encrypt traffic. Logging: errors, access. Monitoring: uptime, performance. Database: connection pooling. Static: CDN. Security headers.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 5 | 10% |
| Intermediate | 45 | 90% |
| Advanced | 0 | 0% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- WSGI standard
- Flask basics and patterns
- Django overview
- FastAPI and type validation
- Templates and Jinja2
- REST API design
- Authentication and sessions
- Middleware and CORS
- Deployment concepts
- Production best practices
