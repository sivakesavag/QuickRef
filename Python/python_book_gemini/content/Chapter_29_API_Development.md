# Chapter 29: API Development

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `requests` (GET, POST, Headers, Auth, Sessions), `json` parsing, HTTP Status Codes, REST Principles, `FastAPI` (Basics, Path/Query Params, Pydantic), `Flask` (Routes), Web Servers (`uvicorn`).

---

**Q29.1: Basic - [Requests Get]**

The most common way to fetch a web page or API endpoint in Python using the `requests` library is:

A) `requests.get('https://example.com')`
B) `requests.fetch('https://example.com')`
C) `http.get('https://example.com')`
D) `urllib.request('https://example.com')`

**Answer: A**

**Explanation:**
Returns a Response object.

---

**Q29.2: Intermediate - [JSON Response]**

If an API returns a JSON response, the easiest way to parse it into a Python dictionary is:

A) `response.json()`
B) `response.dict()`
C) `json.loads(response.text)`
D) `response.parse_json()`

**Answer: A**

**Explanation:**
`requests` provides this helper method (which also handles encoding). Use `json.loads` if you only have the text string.

---

**Q29.3: Advanced - [Status Code 404]**

An HTTP Status Code of `404` indicates:

A) Not Found (the requested resource does not exist).
B) OK (Success).
C) Server Error.
D) Unauthorized.

**Answer: A**

**Explanation:**
200: OK, 401: Unauthorized, 403: Forbidden, 500: Server Error.

---

**Q29.4: Basic - [FastAPI]**

FastAPI is a modern web framework that is primarily known for:

A) High performance (async support) and automatic data validation/documentation using Python type hints.
B) Being slow.
C) Generating HTML only.
D) Database management.

**Answer: A**

**Explanation:**
Built on Starlette and Pydantic.

---

**Q29.5: Intermediate - [Path Parameters]**

In FastAPI/Flask, a route defined as `/users/{user_id}` (FastAPI) or `/users/<user_id>` (Flask) captures `user_id` as a:

A) Path Parameter (variable part of the URL path).
B) Query Parameter.
C) Header.
D) Cookie.

**Answer: A**

**Explanation:**
Used to identify a specific resource.

---

**Q29.6: Advanced - [Requests Session]**

Using `s = requests.Session()` allows you to:

A) Persist parameters (like Cookies, Headers) across multiple requests (e.g., maintaining a login session).
B) Make requests faster.
C) Read the browser history.
D) Open a window.

**Answer: A**

**Explanation:**
Also utilizes connection pooling (TCP reuse) for performance.

---

**Q29.7: Expert - [Pydantic Model]**

In FastAPI, defining a request body using a Pydantic model (`class Item(BaseModel): ...`) ensures:

A) Automatic validation of the incoming JSON data against the model's type hints, and auto-generated Swagger UI documentation.
B) The database is created.
C) The server restarts.
D) Nothing.

**Answer: A**

**Explanation:**
If the client sends invalid data (e.g., string instead of int), FastAPI returns a detailed 422 error automatically.

---

**Q29.8: Basic - [HTTP Verbs]**

Which HTTP Verb is typically used to **create** a new resource?

A) POST
B) GET
C) DELETE
D) HEAD

**Answer: A**

**Explanation:**
GET: Read, PUT: Update (Replace), PATCH: Update (Modify), DELETE: Remove.

---

**Q29.9: Intermediate - [Query Parameters]**

In the URL `https://api.com/items?skip=0&limit=10`, `skip` and `limit` are:

A) Query Parameters.
B) Path Parameters.
C) Domain names.
D) Fragments.

**Answer: A**

**Explanation:**
Separated by `?` and `&`. Used for filtering/sorting/pagination.

---

**Q29.10: Advanced - [Status Code 201]**

The most appropriate status code to return after successfully creating a resource (POST request) is:

A) 201 Created.
B) 200 OK.
C) 204 No Content.
D) 400 Bad Request.

**Answer: A**

**Explanation:**
More specific than 200. Usually comes with a `Location` header.

---

**Q29.11: Basic - [Import Requests]**

To use the `requests` library, you must first:

A) `import requests` (and install it via pip).
B) It is built-in.
C) `import http`
D) `import urllib`

**Answer: A**

**Explanation:**
It is a third-party library (`pip install requests`), though effectively the standard for humans.

---

**Q29.12: Intermediate - [Flask Route]**

In Flask, the decorator to bind a function to a URL is:

A) `@app.route('/path')`
B) `@app.get('/path')`
C) `@app.url('/path')`
D) `@route('/path')`

**Answer: A**

**Explanation:**
e.g., `@app.route('/', methods=['GET', 'POST'])`.

---

**Q29.13: Advanced - [Requests Content]**

`response.content` returns the response body as:

A) Bytes (useful for binary data like images/files).
B) Unicode String.
C) JSON.
D) A list.

**Answer: A**

**Explanation:**
Use `response.text` for the decoded unicode string.

---

**Q29.14: Expert - [FastAPI Async]**

Defining a path operation function with `async def`:

A) Allows FastAPI to run it in the event loop, enabling non-blocking I/O operations (like fetching data from other APIs or DBs asynchronously).
B) Makes it run in a thread.
C) Is mandatory.
D) Is slower.

**Answer: A**

**Explanation:**
If you use standard blocking calls (like `time.sleep`), use normal `def`.

---

**Q29.15: Intermediate - [Headers]**

To send a custom header (e.g., API Key) with `requests`:

A) `requests.get(url, headers={'Authorization': 'Bearer ...'})`
B) `requests.get(url, auth='...')`
C) `requests.header('...')`
D) Put it in the URL.

**Answer: A**

**Explanation:**
The `headers` argument takes a dictionary.

---

**Q29.16: Basic - [Uvicorn]**

`uvicorn` is commonly used with FastAPI to:

A) Run the ASGI application (Serve it).
B) Write the code.
C) Test the code.
D) Database migration.

**Answer: A**

**Explanation:**
"Lightning-fast" ASGI server implementation. `uvicorn main:app --reload`.

---

**Q29.17: Advanced - [Raise for Status]**

`response.raise_for_status()`:

A) Raises an `HTTPError` exception if the status code indicates an error (4xx or 5xx).
B) Raises the server status.
C) Prints the status.
D) Does nothing.

**Answer: A**

**Explanation:**
Best practice to ensure you don't silently process failed requests.

---

**Q29.18: Intermediate - [REST]**

REST (Representational State Transfer) is:

A) An architectural style for designing networked applications (APIs) using standard HTTP methods and stateless communication.
B) A programming language.
C) A database.
D) A sleep mode.

**Answer: A**

**Explanation:**
Resources are identified by URLs.

---

**Q29.19: Basic - [JSON Dump]**

To convert a Python dictionary to a JSON string (serialization):

A) `json.dumps(data)`
B) `json.loads(data)`
C) `json.write(data)`
D) `dict.to_json()`

**Answer: A**

**Explanation:**
`dump` (no s) writes to a file object.

---

**Q29.20: Expert - [Dependency Injection]**

In FastAPI, `Depends()` is used for:

A) Dependency Injection (providing shared logic like DB sessions, authentication, or query extraction to path operations).
B) Listing packages.
C) Installing libraries.
D) Creating dependencies.

**Answer: A**

**Explanation:**
Allows creating reusable components that are automatically resolved by the framework.

---

**Q29.21: Intermediate - [Post Data]**

To send form data (like an HTML form submission) in a POST request:

A) `requests.post(url, data={'key': 'value'})`
B) `requests.post(url, json={'key': 'value'})`
C) `requests.post(url, text='...')`
D) `requests.form(...)`

**Answer: A**

**Explanation:**
Use the `data` argument for `application/x-www-form-urlencoded`. Use `json` for `application/json`.

---

**Q29.22: Basic - [Localhost]**

The standard IP address for "localhost" (the local machine) is:

A) `127.0.0.1`
B) `192.168.1.1`
C) `0.0.0.0`
D) `8.8.8.8`

**Answer: A**

**Explanation:**
Usually maps to `localhost`.

---

**Q29.23: Advanced - [Status Code 500]**

Status Code 500 means:

A) Internal Server Error (The server crashed or encountered a bug).
B) Not Found.
C) Bad Request (Client error).
D) Success.

**Answer: A**

**Explanation:**
It's a server-side issue, not the client's fault.

---

**Q29.24: Expert - [CORS]**

CORS (Cross-Origin Resource Sharing) headers are required when:

A) A frontend web application (JS) running on one domain tries to make an API request to a backend on a *different* domain/port.
B) You run python.
C) You use https.
D) Always.

**Answer: A**

**Explanation:**
Browsers block these requests by default for security unless the server explicitly allows them via `Access-Control-Allow-Origin`.

---

**Q29.25: Intermediate - [Flask Debug]**

Running `app.run(debug=True)` in Flask:

A) Enables the debugger (interactive traceback in browser) and auto-reloader (restarts server on code changes).
B) Makes the app faster.
C) Is for production.
D) Deletes the app.

**Answer: A**

**Explanation:**
NEVER use in production (security risk + performance).

---

**Q29.26: Basic - [Port 80]**

The default port for HTTP traffic is:

A) 80
B) 443
C) 8080
D) 22

**Answer: A**

**Explanation:**
HTTPS is 443. SSH is 22.

---

**Q29.27: Advanced - [Requests Timeout]**

It is good practice to always use `timeout` in requests because:

A) Default requests have no timeout and can hang indefinitely if the server is unresponsive.
B) It makes it faster.
C) It adds a delay.
D) It is required.

**Answer: A**

**Explanation:**
`requests.get(url, timeout=5)`.

---

**Q29.28: Expert - [Middleware]**

Middleware in a web framework (like FastAPI/Flask) is:

A) Code that runs *before* or *after* every request is processed (e.g., logging, error handling, CORS, authentication).
B) The database.
C) The frontend.
D) The hardware.

**Answer: A**

**Explanation:**
It wraps the application logic.

---

**Q29.29: Intermediate - [Swagger UI]**

FastAPI automatically generates interactive API documentation at:

A) `/docs`
B) `/help`
C) `/api`
D) `/swagger`

**Answer: A**

**Explanation:**
Powered by OpenAPI standard.

---

**Q29.30: Basic - [Put vs Patch]**

PUT is generally used for ________, while PATCH is used for ________.

A) Full replacement of the resource; Partial update.
B) Partial update; Full replacement.
C) Creating; Deleting.
D) Reading; Writing.

**Answer: A**

**Explanation:**
PUT expects you to send the *entire* object. PATCH applies a diff.

---

**Q29.31: Intermediate - [Bearer Token]**

To send a Bearer Token (common in OAuth2/JWT) in the Authorization header:

A) `Authorization: Bearer <token>`
B) `Authorization: Token <token>`
C) `Auth: <token>`
D) `Bearer: <token>`

**Answer: A**

**Explanation:**
Standard format. In requests: `headers={'Authorization': f'Bearer {token}'}`.

---

**Q29.32: Advanced - [Idempotency]**

An API method is "Idempotent" if:

A) Making the same request multiple times has the same effect as making it once (e.g., DELETE, PUT).
B) It never fails.
C) It is fast.
D) It uses caching.

**Answer: A**

**Explanation:**
Safe to retry if the network fails. POST is generally *not* idempotent.

---

**Q29.33: Basic - [Cookies]**

Cookies are primarily used to:

A) Store small pieces of data on the client-side (browser) that are sent back to the server with every request (e.g., Session ID).
B) Eat.
C) Run code.
D) Store large files.

**Answer: A**

**Explanation:**
Key mechanism for stateful sessions over stateless HTTP.

---

**Q29.34: Expert - [GraphQL]**

The main difference between GraphQL and REST is:

A) In GraphQL, the client specifies exactly what data structure they need in a single request (avoiding over/under-fetching), whereas REST has fixed endpoints returning fixed structures.
B) GraphQL is older.
C) REST is faster.
D) GraphQL uses XML.

**Answer: A**

**Explanation:**
"Ask for what you need, get exactly that."

---

**Q29.35: Intermediate - [Webhooks]**

A "Webhook" is:

A) A way for an app to provide other applications with real-time information by sending an HTTP POST payload to a pre-configured URL when an event happens (Push vs Pull).
B) A fishing hook.
C) A spider web.
D) A database query.

**Answer: A**

**Explanation:**
"Don't call us, we'll call you."

---

**Q29.36: Advanced - [Rate Limiting]**

Rate Limiting is used to:

A) Control the number of requests a user/client can make to an API within a given timeframe (preventing abuse/overload).
B) Speed up the API.
C) Limit the price.
D) Charge money.

**Answer: A**

**Explanation:**
Returns 429 Too Many Requests if exceeded.

---

**Q29.37: Basic - [HTTPS]**

Why is HTTPS (SSL/TLS) critical for APIs?

A) It encrypts the traffic between client and server, preventing attackers from intercepting sensitive data like passwords or tokens.
B) It is faster.
C) It looks cool.
D) It is free.

**Answer: A**

**Explanation:**
Without it, everything (including Auth headers) is sent in plain text.

---

**Q29.38: Intermediate - [TestClient]**

To test FastAPI or Flask applications without running a real server, you can use:

A) `TestClient` (from Starlette or Flask's test client).
B) `requests.get()`.
C) `selenium`.
D) `ping`.

**Answer: A**

**Explanation:**
Simulates requests directly against the app instance.

---

**Q29.39: Advanced - [API Versioning]**

A common strategy to version APIs is:

A) Including the version in the URL path (e.g., `/v1/users`).
B) Changing the domain.
C) Changing the database.
D) Using cookies.

**Answer: A**

**Explanation:**
Ensures backward compatibility for existing clients when you introduce breaking changes.

---

**Q29.40: Expert - [HATEOAS]**

HATEOAS (Hypermedia as the Engine of Application State) means:

A) API responses include links/hypermedia controls to other related resources, guiding the client on what actions are possible next.
B) The API hates you.
C) The API is stateful.
D) It uses HTML only.

**Answer: A**

**Explanation:**
The "Glory of REST" (Level 3 Richardson Maturity Model), often skipped in practice.

---

**Q29.41: Basic - [Delete Method]**

The HTTP method to remove a resource is:

A) DELETE
B) REMOVE
C) DROP
D) CLEAR

**Answer: A**

**Explanation:**
`requests.delete(url)`.

---

**Q29.42: Intermediate - [Serialization]**

Serialization is the process of:

A) Converting complex objects (like Database Models or Class Instances) into a format suitable for transmission (like JSON strings).
B) Saving to files.
C) Printing.
D) Using serial numbers.

**Answer: A**

**Explanation:**
Deserialization is the reverse.

---

**Q29.43: Advanced - [JWT]**

JWT (JSON Web Token) is commonly used for:

A) Stateless Authentication (the token contains the user identity/claims signed by the server, so the DB doesn't need to be checked for session state on every request).
B) Encryption.
C) Compression.
D) Web design.

**Answer: A**

**Explanation:**
Consists of Header, Payload, Signature.

---

**Q29.44: Expert - [Pagination]**

When an API endpoint returns thousands of records, "Pagination" involves:

A) Returning a subset of results (pages) at a time, often using `limit` and `offset` (or cursor-based) parameters.
B) Printing on paper.
C) Returning everything.
D) Crashing.

**Answer: A**

**Explanation:**
Essential for performance and bandwidth.

---

**Q29.45: Intermediate - [HttpOnly Cookie]**

Setting the `HttpOnly` flag on a cookie:

A) Prevents client-side JavaScript (`document.cookie`) from accessing it, mitigating XSS (Cross-Site Scripting) attacks.
B) Makes it work only on HTTP (not HTTPS).
C) Deletes it.
D) Hides it.

**Answer: A**

**Explanation:**
Best practice for storing sensitive session IDs.

---

**Q29.46: Basic - [Response Headers]**

To access the headers returned by the server:

A) `response.headers`
B) `response.meta`
C) `response.info`
D) `response.top`

**Answer: A**

**Explanation:**
Contains metadata like Content-Type, Date, Server version.

---

**Q29.47: Advanced - [OpenAPI]**

OpenAPI (formerly Swagger) is:

A) A standard specification for defining/documenting REST APIs (endpoints, request/response formats) in a machine-readable format (YAML/JSON).
B) A browser.
C) A server.
D) A database.

**Answer: A**

**Explanation:**
FastAPI generates this automatically.

---

**Q29.48: Expert - [gRPC]**

gRPC is an alternative to REST that uses:

A) Protocol Buffers (binary serialization) and runs over HTTP/2, offering higher performance and strong typing.
B) JSON and HTTP/1.1.
C) XML.
D) Text files.

**Answer: A**

**Explanation:**
Popular in microservices communication.

---

**Q29.49: Intermediate - [Params vs Data]**

In `requests`, the semantic difference is: `params` adds to ________, while `data`/`json` adds to ________.

A) The URL (Query String); The Body.
B) The Body; The URL.
C) The Headers; The Body.
D) The Cookies; The URL.

**Answer: A**

**Explanation:**
`get(url, params=...)` vs `post(url, json=...)`.

---

**Q29.50: Basic - [Mocking]**

In API testing, "Mocking" refers to:

A) Simulating the behavior of external services (like 3rd party APIs) so tests are fast, reliable, and don't hit real servers.
B) Making fun of the API.
C) Copying code.
D) Deleting code.

**Answer: A**

**Explanation:**
`unittest.mock` is invaluable here.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
