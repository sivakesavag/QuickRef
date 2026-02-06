# Chapter 23: Web Development

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: WSGI vs ASGI, Flask (Routing, Contexts, Templates), Django (MVT Architecture, ORM, Middleware), FastAPI (Pydantic models, Async endpoints), Web Servers (Gunicorn/Uvicorn), REST APIs (Methods, JSON), Session Management, Static Files.

---

**Q23.1: Basic - [WSGI Acronym]**

WSGI stands for:

A) Web Server Gateway Interface.
B) Web Standard General Interface.
C) World Standard Gateway Internet.
D) Wide Socket General I/O.

**Answer: A**

**Explanation:**
The standard interface specification (PEP 3333) between Python web applications (Flask, Django) and web servers.

---

**Q23.2: Intermediate - [Flask Route]**

In Flask, to handle both GET and POST methods on a route, you use:

A) `@app.route('/path')` (defaults to all).
B) `@app.route('/path', methods=['GET', 'POST'])`
C) `@app.get_post('/path')`
D) `@app.path('/path')`

**Answer: B**

**Explanation:**
By default, routes only handle GET. You must explicitly list other methods.

---

**Q23.3: Advanced - [Django Middleware]**

Django Middleware is:

A) A hardware component.
B) A framework of hooks into Django's request/response processing (chains of functions that process request before view and response after view).
C) The database layer.
D) The template engine.

**Answer: B**

**Explanation:**
Used for global features like Authentication, Session management, and CSRF protection.

---

**Q23.4: Basic - [FastAPI Validation]**

FastAPI validates request data using:

A) Marshmallow.
B) Django Forms.
C) Pydantic models.
D) Regex manually.

**Answer: C**

**Explanation:**
Pydantic provides runtime type enforcement and auto-generated documentation (Swagger UI).

---

**Q23.5: Intermediate - [ORM Concept]**

ORM (Object-Relational Mapping):

A) Maps Python objects to Database tables (allowing you to write Python code instead of SQL).
B) Maps URLs to Functions.
C) Maps JSON to XML.
D) Optimizes RAM.

**Answer: A**

**Explanation:**
Examples: Django ORM, SQLAlchemy. Eliminates boilerplate SQL.

---

**Q23.6: Advanced - [ASGI vs WSGI]**

The main advantage of ASGI (Asynchronous Server Gateway Interface) over WSGI is:

A) It is older and more stable.
B) It supports asynchronous `async`/`await` capabilities natively (WebSockets, HTTP2, long-polling).
C) It is strictly synchronous.
D) It is simpler.

**Answer: B**

**Explanation:**
WSGI is synchronous (blocking). ASGI is designed for modern async Python web apps (like FastAPI, Django Channels).

---

**Q23.7: Basic - [Gunicorn]**

Gunicorn is:

A) A Python Web Framework.
B) A production-grade WSGI HTTP Server.
C) A database.
D) A template.

**Answer: B**

**Explanation:**
It runs your Python app (Flask/Django) in multiple worker processes to handle traffic.

---

**Q23.8: Intermediate - [Flask Context]**

The `g` object in Flask (`from flask import g`) is used for:

A) Global data shared across all users/requests (unsafe).
B) Storing data temporarily for the *current request* cycle only (global within the request context).
C) Google Login.
D) Graphics.

**Answer: B**

**Explanation:**
Good for storing database connections or user info specific to the one pending request.

---

**Q23.9: Advanced - [Django MVT]**

Django's architecture is MVT, which stands for:

A) Model View Template.
B) Model View Controller.
C) Main Valid Time.
D) Micro Virtual Thread.

**Answer: A**

**Explanation:**
Similar to MVC, but in Django the "View" handles the business logic (Controller), and "Template" handles the presentation (View).

---

**Q23.10: Expert - [Cookies vs LocalStorage]**

For security, HttpOnly Cookies are generally preferred over LocalStorage for storing auth tokens because:

A) LocalStorage is slower.
B) LocalStorage is accessible to any JavaScript running on the page (Vulnerable to XSS). HttpOnly properties prevent JS access.
C) Cookies hold more data.
D) LocalStorage deletes on close.

**Answer: B**

**Explanation:**
If an attacker injects JS (XSS), they can dump LocalStorage. They cannot read HttpOnly cookies.

---

**Q23.11: Basic - [Uvicorn]**

To run a FastAPI application (ASGI), you typically use:

A) Gunicorn (alone).
B) Uvicorn (an ASGI server).
C) Apache.
D) IIS.

**Answer: B**

**Explanation:**
Uvicorn is a lightning-fast ASGI server implementation, often managed by Gunicorn in production.

---

**Q23.12: Intermediate - [Django Migrations]**

`python manage.py make_migrations` does what?

A) Creates the database tables.
B) Creates migration files describing changes to your models (Git-trackable schema evolution).
C) Deletes the DB.
D) Runs the server.

**Answer: B**

**Explanation:**
It *plans* the changes. `migrate` *applies* them to the actual DB.

---

**Q23.13: Advanced - [REST Idempotency]**

In REST API design, which method is NOT idempotent?

A) GET
B) PUT (Replace resource)
C) DELETE
D) POST (Create resource)

**Answer: D**

**Explanation:**
Repeating a POST request multiple times creates multiple resources. PUT/DELETE repeating has the same result state.

---

**Q23.14: Basic - [Jinja2]**

Jinja2 is:

A) A Japanese game.
B) The default Templating Engine for Flask.
C) An ORM.
D) A database.

**Answer: B**

**Explanation:**
Allows embedding python-like syntax (`{{ variable }}`) in HTML files.

---

**Q23.15: Intermediate - [Django Select Related]**

`Model.objects.select_related('foreign_key')` is an optimization that:

A) Selects random rows.
B) Performs a SQL JOIN to fetch related data in a single query (preventing N+1 query problem).
C) Deletes related rows.
D) Slows down queries.

**Answer: B**

**Explanation:**
Crucial for performance. Without it, accessing `obj.foreign_key` inside a loop would trigger a new DB query for every item.

---

**Q23.16: Advanced - [Flask Blueprints]**

Flask Blueprints are used to:

A) Design the UI.
B) Organize a Flask application into modular components (splitting routes into multiple files).
C) Print the code.
D) Database design.

**Answer: B**

**Explanation:**
Allows scaling a Flask app beyond a single `app.py` file.

---

**Q23.17: Expert - [GraphQL vs REST]**

A key difference between GraphQL and REST is:

A) GraphQL uses XML.
B) GraphQL allows the client to specify exactly what fields it needs (preventing over-fetching), whereas REST endpoints typically return fixed structures.
C) REST is faster.
D) They are identical.

**Answer: B**

**Explanation:**
GraphQL provides a flexible single endpoint; REST uses multiple endpoints with fixed schemas.

---

**Q23.18: Intermediate - [Session Source]**

Server-side sessions (e.g., Flask default session) typically store data:

A) Encrypted/Signed in the Browser Cookie.
B) In the server RAM only.
C) In a text file on user desktop.
D) Nowhere.

**Answer: A**

**Explanation:**
Flask's default session is a crypto-signed cookie. Django's default session stores data in the DB and the ID in the cookie.

---

**Q23.19: Basic - [Static Files]**

"Static Files" in web development refer to:

A) Python scripts.
B) Files that don't change dynamically (CSS, JavaScript, Images) served directly to the client.
C) Locked files.
D) Database files.

**Answer: B**

**Explanation:**
Efficiently served by Nginx/Apache/CDN, avoiding Python overhead.

---

**Q23.20: Advanced - [CSRF Token]**

A CSRF Token protects against:

A) Cross-Site Scripting.
B) Cross-Site Request Forgery (Attacker forces a logged-in user's browser to send an unwanted action).
C) SQL Injection.
D) Password theft.

**Answer: B**

**Explanation:**
The server validates that the POST request contains a secret token known only to the user's current session view.

---

**Q23.21: EXPERT - [ASGI Lifespan]**

The ASGI Lifespan protocol is used for:

A) Determining how long the server runs.
B) Handling startup and shutdown events (e.g., initializing DB connections) in an async context.
C) Timing requests.
D) Logging.

**Answer: B**

**Explanation:**
Replaces the old `on_start` hooks, providing a standard async context manager for the application lifecycle.

---

**Q23.22: Intermediate - [Django Admin]**

Django's "Killer Feature" out of the box is:

A) Its speed.
B) The Automatic Admin Interface (auto-generated CRUD UI).
C) NoSQL support.
D) Microservices.

**Answer: B**

**Explanation:**
Massively speeds up internal tool development.

---

**Q23.23: Basic - [Localhost Port]**

By default, Flask runs on port `5000`, Django on:

A) 3000
B) 8080
C) 8000
D) 80

**Answer: C**

**Explanation:**
Standard default development ports.

---

**Q23.24: Advanced - [Websockets]**

WebSockets provide:

A) Faster HTTP requests.
B) Full-duplex communication channel over a single TCP connection (Real-time bidirectional data).
C) Wireless connection.
D) Security only.

**Answer: B**

**Explanation:**
Unlike HTTP (Request-Response), the server can push messages to the client at any time.

---

**Q23.25: Intermediate - [SQLAlchemy vs Django ORM]**

A primary design difference is SQLAlchemy uses the "Data Mapper" pattern, while Django ORM uses:

A) Active Record pattern.
B) Passive Record.
C) No pattern.
D) Raw SQL.

**Answer: A**

**Explanation:**
In Active Record (Django), the model class itself has methods to save/delete instances (`user.save()`).

---

**Q23.26: Basic - [Flask Request Object]**

`flask.request`:

A) Is a global variable available everywhere continuously.
B) Is a proxy object that points to the request data of the current handling thread/context.
C) Is a new instance passed to every function.
D) Is static.

**Answer: B**

**Explanation:**
It uses "Context Locals" to look like a global but actually maps to the specific request for the current thread.

---

**Q23.27: Expert - [Nginx Reverse Proxy]**

In a production Python web deployment, Nginx is typically placed *in front* of Gunicorn/Uvicorn to:

A) Run Python code.
B) Handle SSL termination, serve static files, and buffer slow clients (Reverse Proxy), protecting the Python application server.
C) Edit the code.
D) Debug.

**Answer: B**

**Explanation:**
Python servers (Gunicorn) are not designed to be exposed directly to the public internet (slow loris attacks, etc.).

---

**Q23.28: Advanced - [Content Negotiation]**

The HTTP Header `Accept: application/json` tells the server:

A) The client sends JSON.
B) The client expects/prefers a JSON response.
C) The server must crash.
D) To accept the connection.

**Answer: B**

**Explanation:**
Allows a single endpoint to serve HTML or JSON depending on client request.

---

**Q23.29: Intermediate - [FastAPI Dependency Injection]**

FastAPI's dependency injection system (`Depends`):

A) Downloads libraries.
B) Allows manageable code reuse for logic like database sessions, authentication, or query params, which are "injected" into route functions.
C) Is slow.
D) Is complicated.

**Answer: B**

**Explanation:**
A core feature that makes FastAPI modular and testable.

---

**Q23.30: Basic - [404 Error]**

HTTP 404 means:

A) Server Error.
B) Forbidden.
C) Not Found.
D) OK.

**Answer: C**

**Explanation:**
The requested resource could not be found.

---

**Q23.31: Intermediate - [Flask Session Secret]**

If you don't set `app.secret_key` in Flask, using sessions will:

A) Work without security.
B) Raise a RuntimeError (The session is unavailable because no secret key was set).
C) Use a default key "flask".
D) Be perfectly safe.

**Answer: B**

**Explanation:**
Flask requires a secret key to sign the session cookie to prevent tampering.

---

**Q23.32: Advanced - [Django F Expression]**

`from django.db.models import F`. `F` objects allow you to:

A) Filter by nothing.
B) Reference the value of a model field *in the database* directly (e.g., atomic increments `quantity = F('quantity') + 1`).
C) Format dates.
D) Find files.

**Answer: B**

**Explanation:**
Prevents race conditions where fetching, incrementing in Python, and saving would overwrite parallel updates.

---

**Q23.33: Basic - [Uvicorn Workers]**

To run Uvicorn with multiple workers in production, you generally use:

A) `uvicorn main:app --reload`
B) A process manager like Gunicorn with Uvicorn workers (`gunicorn -k uvicorn.workers.UvicornWorker ...`).
C) Threading.
D) Forking manually.

**Answer: B**

**Explanation:**
Uvicorn is an ASGI worker class. Gunicorn manages the worker processes.

---

**Q23.34: Expert - [FastAPI Background Tasks]**

FastAPI's `BackgroundTasks` run:

A) In a separate process (Celery).
B) In the same event loop, *after* the response has been sent to the client.
C) Before the response.
D) In a thread.

**Answer: B**

**Explanation:**
Useful for lightweight tasks (sending email, logging) without blocking the user response, but for heavy CPu tasks, use Celery/RQ.

---

**Q23.35: Intermediate - [REST Status 201]**

The HTTP status code `201` is specifically for:

A) OK.
B) Created (successful resource creation via POST).
C) Accepted.
D) No Content.

**Answer: B**

**Explanation:**
Indicates the POST request succeeded and a new resource exists.

---

**Q23.36: Advanced - [Django Signals]**

Django Signals (`post_save`, `pre_delete`) allows:

A) Wireless communication.
B) Decoupled components to get notified when generic actions occur (e.g., creating a profile when a User is saved).
C) Stopping the server.
D) Database signaling.

**Answer: B**

**Explanation:**
Useful for side effects, though overusing them makes logic hard to trace.

---

**Q23.37: Basic - [Endpoint Security]**

The most common way to secure a REST API today is:

A) HTTP Basic Auth (Username/Password).
B) OAuth2 / JWT (JSON Web Tokens).
C) IP Whitelisting only.
D) No security.

**Answer: B**

**Explanation:**
Stateless tokens (JWT) are preferred for modern APIs over session cookies or basic auth.

---

**Q23.38: Intermediate - [Flask Before Request]**

`@app.before_request`:

A) Registers a function to run before *every* request (e.g., opening DB connection, checking login).
B) Runs once at startup.
C) Runs after request.
D) Runs only on errors.

**Answer: A**

**Explanation:**
Global hook for request setup.

---

**Q23.39: Advanced - [CORS]**

CORS (Cross-Origin Resource Sharing) headers are set by the **server** to:

A) Protect the server from the client.
B) Allow (or block) web browsers from making requests to the server from a different domain (Origin).
C) Speed up the internet.
D) Compress JSON.

**Answer: B**

**Explanation:**
By default, browsers block cross-origin AJAX requests. `Access-Control-Allow-Origin` relaxes this.

---

**Q23.40: Expert - [Database Transaction Atomic]**

`with transaction.atomic():` in Django:

A) Locks the entire database.
B) Guarantees that all DB operations inside the block either all succeed (commit) or all fail (rollback).
C) Splits the atom.
D) Is only for Postgres.

**Answer: B**

**Explanation:**
Ensures data integrity. If an error occurs halfway, no partial data is written.

---

**Q23.41: Basic - [HTML Response]**

To return HTML from a view function:

A) Return a string of HTML code (or render a template).
B) Return a dictionary.
C) Return an integer.
D) Return None.

**Answer: A**

**Explanation:**
Browsers render the string body as HTML if `Content-Type: text/html` is set (default in Flask/Django render).

---

**Q23.42: Intermediate - [Django QuerySet Lazy]**

Django QuerySets are lazy, meaning:

A) They execute the SQL immediately.
B) They don't run the SQL query until the data is actually evaluated (iterated over, sliced, or printed).
C) They are slow.
D) They never run.

**Answer: B**

**Explanation:**
Allows chaining filters `User.objects.filter(active=True).filter(age__gt=18)` without hitting the DB multiple times.

---

**Q23.43: Advanced - [Web Server Gateway]**

Nginx communicates with Gunicorn via:

A) HTTP over a UNIX socket or TCP port (Proxy Pass).
B) Direct memory access.
C) Python API.
D) Telepathy.

**Answer: A**

**Explanation:**
It acts as a reverse proxy, forwarding the raw HTTP request to the upstream Gunicorn server.

---

**Q23.44: Expert - [Slow Loris]**

A "Slow Loris" attack works by:

A) Sending huge requests.
B) Opening many connections and keeping them open as long as possible by sending partial headers slowly, exhausting the server's thread pool.
C) SQL Injection.
D) deleting database.

**Answer: B**

**Explanation:**
Why async servers or buffering reverse proxies (Nginx) are needed in front of sync workers (Gunicorn) which have limited worker pools.

---

**Q23.45: Intermediate - [FastAPI Docs]**

FastAPI automatically generates interactive API documentation at:

A) `/docs` (Swagger UI) and `/redoc`.
B) `/help`.
C) It does not generate docs.
D) `/api`.

**Answer: A**

**Explanation:**
Leverages OpenAPI standard and Pydantic types.

---

**Q23.46: Basic - [HTTP Port SSL]**

Standard port for HTTPS:

A) 80
B) 443
C) 8080
D) 25

**Answer: B**

**Explanation:**
Port 443.

---

**Q23.47: Advanced - [Caching Headers]**

The `Cache-Control` header `max-age=3600` tells the client:

A) The server is 3600 years old.
B) To cache the response for 3600 seconds (1 hour) before requesting it again.
C) To delete the file after 1 hour.
D) To wait 1 hour.

**Answer: B**

**Explanation:**
Critical for performance, reducing server load for static or semi-static content.

---

**Q23.48: Expert - [ASGI WebSocket]**

In ASGI, a WebSocket connection typically involves three event types:

A) connect, receive, disconnect.
B) get, post, put.
C) open, read, write.
D) start, stop, pause.

**Answer: A**

**Explanation:**
The application awaits `send` and `receive` events to handle the full-duplex traffic.

---

**Q23.49: Intermediate - [Django Class Based Views]**

CBVs (Class-Based Views) in Django (e.g., `ListView`, `CreateView`) are used to:

A) Write more code.
B) Reuse common logic (boilerplate) through inheritance (OOP) rather than writing repetitive function views.
C) Make views slower.
D) Deprecate functions.

**Answer: B**

**Explanation:**
Standard way to implement generic CRUD views quickly.

---

**Q23.50: Basic - [Server Error]**

HTTP 500 means:

A) Not Found.
B) Internal Server Error (The Python code crashed/raised an unhandled exception).
C) Bad Request.
D) Unauthorized.

**Answer: B**

**Explanation:**
Generic error message when the server fails to handle the request.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
