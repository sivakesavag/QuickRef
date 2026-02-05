# Chapter 18: Networking & HTTP

> **Topics Covered**: socket programming, urllib, requests library, HTTP methods, REST APIs, JSON APIs, authentication, sessions, async HTTP with aiohttp, websockets basics, error handling

---

## Questions

---

**Q18.1: Basic - [TCP vs UDP]**

What's the main difference between TCP and UDP?

A) TCP is faster
B) TCP is connection-oriented with guaranteed delivery; UDP is connectionless, faster but unreliable
C) UDP is outdated
D) No real difference

**Answer: B**

**Explanation:**
TCP: connection established first, ordered delivery, retransmission on failure. HTTP uses TCP. UDP: no connection, packets may arrive out-of-order or not at all. Used for streaming, games where speed > reliability.

---

**Q18.2: Basic - [socket Basics]**

What does `socket.socket()` create?

A) Network cable
B) Endpoint for network communication
C) HTTP server
D) URL connection

**Answer: B**

**Explanation:**
`socket.socket(AF_INET, SOCK_STREAM)` creates TCP socket. AF_INET = IPv4. SOCK_STREAM = TCP. SOCK_DGRAM = UDP. Socket is bidirectional communication endpoint. Low-level networking.

---

**Q18.3: Intermediate - [Socket Server]**

What's the sequence for a TCP server socket?
```python
s = socket.socket(AF_INET, SOCK_STREAM)
# What's next?
```

A) connect → send → recv
B) bind → listen → accept → recv/send
C) listen → bind → accept
D) send → recv → close

**Answer: B**

**Explanation:**
Server: `bind((host, port))` → `listen(backlog)` → `accept()` returns (conn, addr) → `recv()/send()` on conn → `close()`. Client: `connect((host, port))` → `recv()/send()`.

---

**Q18.4: Intermediate - [urllib.request]**

What is the output?
```python
from urllib.request import urlopen
with urlopen('http://example.com') as response:
    print(type(response.read()))
```

A) `<class 'str'>`
B) `<class 'bytes'>`
C) `<class 'Response'>`
D) `<class 'dict'>`

**Answer: B**

**Explanation:**
`urlopen()` returns HTTPResponse. `read()` returns body as bytes. Decode for string: `response.read().decode('utf-8')`. Standard library HTTP client, but `requests` is more user-friendly.

---

**Q18.5: Intermediate - [requests Library]**

What is the output?
```python
import requests
r = requests.get('https://api.example.com/data')
print(type(r), type(r.text), type(r.content))
```

A) `Response, str, bytes`
B) `str, str, str`
C) `bytes, str, bytes`
D) Error

**Answer: A**

**Explanation:**
`requests.get()` returns Response object. `r.text` = decoded string. `r.content` = raw bytes. `r.json()` = parsed JSON (if applicable). `r.status_code` = HTTP status. Much cleaner than urllib.

---

**Q18.6: Basic - [HTTP Methods]**

Match HTTP methods to actions:

A) GET=create, POST=read
B) GET=read, POST=create, PUT=update, DELETE=delete
C) All methods do the same
D) GET=delete, DELETE=get

**Answer: B**

**Explanation:**
RESTful conventions: GET (retrieve), POST (create), PUT (replace), PATCH (partial update), DELETE (remove). GET should be safe (no side effects). POST/PUT/DELETE modify data.

---

**Q18.7: Intermediate - [requests.post]**

What is the output?
```python
import requests
r = requests.post('https://httpbin.org/post', 
                  json={'key': 'value'})
print(r.status_code)
```

A) `200`
B) `201`
C) Error
D) `404`

**Answer: A**

**Explanation:**
`json=` parameter sends JSON body with correct Content-Type header. httpbin.org echoes back. Returns 200 (or 201 for actual creation). `data=` sends form-encoded data instead.

---

**Q18.8: Intermediate - [HTTP Status Codes]**

What do these status code ranges mean? 2xx, 4xx, 5xx

A) All are errors
B) 2xx=success, 4xx=client error, 5xx=server error
C) 2xx=redirect, 4xx=success, 5xx=info
D) Random numbers

**Answer: B**

**Explanation:**
200 OK, 201 Created, 204 No Content. 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found. 500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable. Know common codes.

---

**Q18.9: Intermediate - [r.raise_for_status()]**

What does `r.raise_for_status()` do?

A) Prints status
B) Raises HTTPError if status is 4xx or 5xx
C) Returns status
D) Always raises error

**Answer: B**

**Explanation:**
Without it, even 404 returns silently. `raise_for_status()` raises exception for error statuses. Use in try/except for error handling: `try: r.raise_for_status() except requests.HTTPError:`.

---

**Q18.10: Intermediate - [Query Parameters]**

What is the output?
```python
import requests
r = requests.get('https://api.example.com/search',
                 params={'q': 'python', 'page': 1})
print(r.url)
```

A) `https://api.example.com/search`
B) `https://api.example.com/search?q=python&page=1`
C) Error
D) `{'q': 'python', 'page': 1}`

**Answer: B**

**Explanation:**
`params=` dict becomes query string. Properly URL-encoded. Cleaner than manual string concatenation. Handles special characters: `{'q': 'a b'}` → `q=a%20b`.

---

**Q18.11: Intermediate - [Headers]**

What is the output?
```python
import requests
r = requests.get('https://api.example.com',
                 headers={'Authorization': 'Bearer token123'})
print('Authorization' in r.request.headers)
```

A) `True`
B) `False`
C) Error
D) `'Bearer token123'`

**Answer: A**

**Explanation:**
`headers=` dict adds/overrides HTTP headers. Common: Authorization, Content-Type, Accept. `r.request.headers` shows what was sent. `r.headers` shows response headers.

---

**Q18.12: Intermediate - [JSON Response]**

What is the output?
```python
import requests
r = requests.get('https://api.github.com')
data = r.json()
print(type(data))
```

A) `<class 'str'>`
B) `<class 'dict'>`
C) `<class 'bytes'>`
D) Error

**Answer: B**

**Explanation:**
`r.json()` parses JSON response body to Python dict/list. Raises JSONDecodeError if invalid JSON. Check `r.headers['Content-Type']` to verify JSON response expected.

---

**Q18.13: Intermediate - [Timeout]**

Why is `timeout` parameter important?

A) Makes requests faster
B) Prevents hanging indefinitely on slow/dead servers
C) Required for security
D) Sets server timeout

**Answer: B**

**Explanation:**
`requests.get(url, timeout=5)` — fail after 5 seconds. Without timeout, requests can hang forever. Always set timeouts in production: `timeout=(connect_timeout, read_timeout)`.

---

**Q18.14: Intermediate - [Sessions]**

What is the advantage of `requests.Session()`?

A) Faster single requests
B) Persists cookies, connection reuse, consistent settings across requests
C) More secure
D) Required for HTTPS

**Answer: B**

**Explanation:**
```python
with requests.Session() as s:
    s.headers['Authorization'] = 'Bearer token'
    s.get(url1)  # Uses header
    s.get(url2)  # Uses same header, cookies persist
```
Connection pooling, persistent cookies, consistent config. More efficient for multiple requests.

---

**Q18.15: Intermediate - [Authentication]**

What does this do?
```python
import requests
r = requests.get(url, auth=('user', 'pass'))
```

A) URL authentication
B) HTTP Basic Auth — sends credentials in Authorization header
C) OAuth login
D) Cookie auth

**Answer: B**

**Explanation:**
`auth=` tuple sends HTTP Basic Authentication (base64-encoded username:password). For Bearer tokens: use `headers={'Authorization': 'Bearer token'}`. For OAuth, use dedicated libraries.

---

**Q18.16: Intermediate - [File Upload]**

What does this do?
```python
import requests
files = {'file': open('doc.pdf', 'rb')}
r = requests.post(url, files=files)
```

A) Downloads file
B) Uploads file as multipart/form-data
C) Sends file path
D) Error

**Answer: B**

**Explanation:**
`files=` for multipart file upload. Proper Content-Type automatically set. Can include multiple files, add filename/content-type: `files={'file': ('name.pdf', file_obj, 'application/pdf')}`.

---

**Q18.17: Intermediate - [Connection Pooling]**

How does requests handle multiple requests to same host?

A) New connection each time
B) Session reuses connections (HTTP keep-alive)
C) Always HTTP/2
D) No optimization

**Answer: B**

**Explanation:**
`Session` maintains connection pool. HTTP/1.1 keep-alive reuses TCP connections. Reduces latency for multiple requests. Without Session, connections may still be reused via urllib3 pool.

---

**Q18.18: Intermediate - [Streaming Response]**

When use `stream=True` in requests?

A) For video streaming
B) For large downloads — don't load entire response into memory
C) For faster requests
D) For WebSockets

**Answer: B**

**Explanation:**
```python
with requests.get(url, stream=True) as r:
    for chunk in r.iter_content(chunk_size=8192):
        process(chunk)
```
Large files: stream and save incrementally. Without stream, entire response loads to memory. `iter_lines()` for text streaming.

---

**Q18.19: Intermediate - [SSL Verification]**

What does `verify=False` do?

A) Faster requests
B) Disables SSL certificate verification (security risk!)
C) Verifies SSL
D) Nothing

**Answer: B**

**Explanation:**
⚠️ `verify=False` skips certificate validation — vulnerable to MITM attacks. Only use for testing with self-signed certs. `verify='/path/to/cert.pem'` for custom CA. Default `verify=True` is correct.

---

**Q18.20: Intermediate - [Retries]**

How to add automatic retries with requests?

A) Built-in retry loop
B) Use urllib3 Retry adapter with Session
C) try/except loop manually
D) Not possible

**Answer: B**

**Explanation:**
```python
from urllib3.util.retry import Retry
from requests.adapters import HTTPAdapter
s = Session()
s.mount('http://', HTTPAdapter(max_retries=Retry(total=3, backoff_factor=1)))
```
Retries on connection errors, configurable status codes. Production-ready HTTP handling.

---

**Q18.21: Intermediate - [aiohttp Basics]**

What is `aiohttp` for?

A) Faster sync requests
B) Async HTTP client/server compatible with asyncio
C) Alternative to requests
D) HTTP/2 only

**Answer: B**

**Explanation:**
`aiohttp` for async HTTP. `async with aiohttp.ClientSession() as session: async with session.get(url) as r:`. Enables concurrent HTTP requests with asyncio. Used in async applications.

---

**Q18.22: Intermediate - [aiohttp Example]**

What is the benefit of this pattern?
```python
async def fetch_all(urls):
    async with aiohttp.ClientSession() as session:
        tasks = [session.get(url) for url in urls]
        responses = await asyncio.gather(*tasks)
```

A) Sequential requests
B) Concurrent requests — all URLs fetched simultaneously
C) Parallel requests (multi-core)
D) No benefit

**Answer: B**

**Explanation:**
All requests start at once, complete concurrently. If each takes 1 second, fetching 100 URLs takes ~1 second, not 100. Essential for high-performance async applications.

---

**Q18.23: Intermediate - [WebSocket Basics]**

What are WebSockets for?

A) Socket.io only
B) Full-duplex persistent connection for real-time bidirectional communication
C) Faster HTTP
D) File sockets

**Answer: B**

**Explanation:**
WebSocket: persistent connection, server can push data anytime. Unlike HTTP request-response. Use for: chat, live updates, games. `websocket-client` or `websockets` (async) libraries in Python.

---

**Q18.24: Intermediate - [REST API Best Practices]**

What's the correct endpoint design for getting user with ID 123?

A) `POST /getUser?id=123`
B) `GET /users/123`
C) `GET /user?action=get&id=123`
D) `READ /users/123`

**Answer: B**

**Explanation:**
RESTful: resources as nouns, HTTP methods as verbs. `/users/123` identifies resource. GET for retrieval. POST `/users` to create. PUT `/users/123` to update. Clean, predictable URLs.

---

**Q18.25: Intermediate - [Content-Type Header]**

What Content-Type for JSON?

A) `text/plain`
B) `application/json`
C) `text/json`
D) `data/json`

**Answer: B**

**Explanation:**
`application/json` for JSON data. `application/x-www-form-urlencoded` for form data. `multipart/form-data` for file uploads. `text/html` for HTML. Check and set correctly.

---

**Q18.26: Intermediate - [CORS]**

What is CORS?

A) Server security
B) Cross-Origin Resource Sharing — browser security for cross-domain requests
C) Caching
D) Compression

**Answer: B**

**Explanation:**
Browser restricts JavaScript from making requests to different domains. Server sets `Access-Control-Allow-Origin` header to permit. Not relevant for server-side Python, but matters when your API is called from browsers.

---

**Q18.27: Intermediate - [URL Encoding]**

What is the output?
```python
from urllib.parse import urlencode
print(urlencode({'name': 'John Doe', 'city': 'New York'}))
```

A) `name=John Doe&city=New York`
B) `name=John+Doe&city=New+York`
C) `{'name': 'John Doe'}`
D) Error

**Answer: B**

**Explanation:**
`urlencode` converts dict to query string with URL encoding. Spaces become `+` (or `%20`). Special characters escaped. `quote()` for individual strings. `parse_qs()` for reverse.

---

**Q18.28: Intermediate - [Parsing URLs]**

What is the output?
```python
from urllib.parse import urlparse
result = urlparse('https://example.com:8080/path?q=1')
print(result.netloc, result.path)
```

A) `example.com, /path`
B) `example.com:8080, /path`
C) `https, example.com:8080`
D) Error

**Answer: B**

**Explanation:**
`urlparse` splits URL into components. `scheme` = 'https'. `netloc` = 'example.com:8080'. `path` = '/path'. `query` = 'q=1'. Also: `hostname`, `port` for parsed netloc.

---

**Q18.29: Intermediate - [API Rate Limiting]**

What should you do when API returns 429 Too Many Requests?

A) Retry immediately
B) Check Retry-After header, implement backoff
C) Ignore and continue
D) Use different API

**Answer: B**

**Explanation:**
429 = rate limited. `Retry-After` header tells wait time. Implement exponential backoff. Respect API limits. Cache responses when possible. Some libraries handle automatically.

---

**Q18.30: Intermediate - [Response Caching]**

How to cache HTTP responses?

A) Automatic in requests
B) Use requests-cache, CacheControl, or implement manually with headers
C) Not possible
D) Built into HTTP

**Answer: B**

**Explanation:**
`requests-cache` adds transparent caching. Respects Cache-Control, ETag, Last-Modified headers. Reduces requests, speeds up. Configure cache backend (memory, sqlite, redis).

---

**Q18.31: Intermediate - [API Pagination]**

How do APIs typically handle large datasets?

A) Return everything
B) Pagination — return pages with limit/offset or cursor
C) Compression only
D) Multiple endpoints

**Answer: B**

**Explanation:**
`GET /items?page=2&per_page=50` or `GET /items?cursor=abc123`. Response includes: items, total count, next page link. Iterate through pages to get all data. Prevents massive single responses.

---

**Q18.32: Intermediate - [Error Handling Pattern]**

What's a robust pattern for API requests?
```python
try:
    r = requests.get(url, timeout=10)
    r.raise_for_status()
    return r.json()
except requests.exceptions.ConnectionError:
    # handle
except requests.exceptions.Timeout:
    # handle
except requests.exceptions.HTTPError:
    # handle
```

A) Overkill
B) Proper exception handling for different failure modes
C) Only try/except needed
D) No error handling needed

**Answer: B**

**Explanation:**
Different errors need different handling. Connection error: retry or fallback. Timeout: increase or alert. HTTPError: check status code, log. JSONDecodeError: invalid response. Comprehensive handling for production.

---

**Q18.33: Intermediate - [Proxy Settings]**

How to use a proxy with requests?

A) `requests.get(url, proxy=addr)`
B) `requests.get(url, proxies={'http': 'http://proxy:8080', 'https': 'https://proxy:8080'})`
C) Environment variable only
D) Not supported

**Answer: B**

**Explanation:**
`proxies=` dict with http/https URLs. Also reads `HTTP_PROXY`, `HTTPS_PROXY` environment variables. For SOCKS: `pip install requests[socks]`. Used for corporate networks, anonymity.

---

**Q18.34: Intermediate - [HTTP/2]**

Does requests support HTTP/2?

A) Yes, by default
B) No, use httpx for HTTP/2 support
C) With plugin
D) HTTP/2 doesn't exist

**Answer: B**

**Explanation:**
`requests` is HTTP/1.1 only. `httpx` supports HTTP/2, async, similar API. `aiohttp` focuses on async HTTP/1.1. HTTP/2 has multiplexing, server push — better for many concurrent requests.

---

**Q18.35: Intermediate - [httpx Example]**

What does httpx offer over requests?

A) Nothing
B) HTTP/2, async support, modern API, same sync interface
C) Different language
D) Only async

**Answer: B**

**Explanation:**
`httpx`: drop-in replacement for requests (similar API), plus HTTP/2, `async with httpx.AsyncClient()`. Modern choice for new projects. `pip install httpx`.

---

**Q18.36: Intermediate - [API Key Authentication]**

Common ways to send API keys:

A) URL only
B) Query param, header (Authorization or X-API-Key), request body
C) Cookies only
D) No standard

**Answer: B**

**Explanation:**
Query: `?api_key=xxx` (less secure — logged). Header: `Authorization: Bearer xxx` or `X-API-Key: xxx` (preferred). Body: sometimes for POST. Check API docs for required method.

---

**Q18.37: Intermediate - [OAuth 2.0]**

What is OAuth 2.0?

A) Password authentication
B) Authorization framework for delegated access without sharing passwords
C) HTTP version
D) Encryption

**Answer: B**

**Explanation:**
OAuth: user authorizes app to access their data on another service. App gets token, not password. Flows: Authorization Code, Client Credentials, etc. Libraries: `oauthlib`, `requests-oauthlib`.

---

**Q18.38: Intermediate - [Bearer Token]**

What does `Authorization: Bearer <token>` mean?

A) File bearer
B) Token-based authentication — include token in header for API access
C) Basic auth
D) Cookie

**Answer: B**

**Explanation:**
Bearer token: proof of authorization. Typically JWT or opaque string from OAuth flow. Include in every request. Server validates token. Most common modern API auth pattern.

---

**Q18.39: Intermediate - [JSON Web Tokens]**

What is a JWT?

A) JavaScript token
B) Self-contained token with encoded claims, signature for verification
C) Encrypted password
D) Cookie

**Answer: B**

**Explanation:**
JWT = Header.Payload.Signature (base64 encoded). Contains claims (user ID, expiration). Signature verifies integrity. Self-contained — server doesn't need session storage. `pyjwt` library to encode/decode.

---

**Q18.40: Intermediate - [socket.gethostbyname]**

What is the output?
```python
import socket
print(socket.gethostbyname('localhost'))
```

A) `localhost`
B) `127.0.0.1`
C) `0.0.0.0`
D) Error

**Answer: B**

**Explanation:**
`gethostbyname` resolves hostname to IP. 'localhost' typically resolves to `127.0.0.1`. `gethostname()` returns machine's hostname. DNS resolution for networking.

---

**Q18.41: Intermediate - [Keep-Alive]**

What is HTTP Keep-Alive?

A) Health check
B) Persistent connection — multiple requests over single TCP connection
C) Session persistence
D) Heartbeat

**Answer: B**

**Explanation:**
HTTP/1.1 default: Keep-Alive. One TCP handshake, multiple requests. Avoids connection overhead. `Connection: close` to disable. Sessions in requests leverage this automatically.

---

**Q18.42: Intermediate - [Response Time]**

How to measure request time with requests?

A) Manual timer
B) `r.elapsed` returns timedelta
C) Not available
D) Calculate from timestamp

**Answer: B**

**Explanation:**
`r.elapsed` is `timedelta` from sending request to receiving response (headers). For full time including content download, use manual timing with `time.time()` before/after.

---

**Q18.43: Intermediate - [Multipart Form]**

When is `multipart/form-data` needed?

A) All POST requests
B) File uploads, or form data with binary content
C) JSON APIs
D) GET requests

**Answer: B**

**Explanation:**
Multipart: separates form fields and files. `requests.post(url, files=...)` uses multipart. JSON APIs use `application/json`. Standard forms use `application/x-www-form-urlencoded`.

---

**Q18.44: Intermediate - [Redirect Handling]**

What does `allow_redirects=False` do?

A) Faster requests
B) Doesn't follow HTTP redirects automatically
C) Prevents all navigation
D) Error on redirect

**Answer: B**

**Explanation:**
Default: follows 3xx redirects automatically. `allow_redirects=False`: returns redirect response, doesn't follow. Check `r.is_redirect`, `r.headers['Location']`. Useful when you need redirect logic control.

---

**Q18.45: Intermediate - [Email with smtplib]**

What does smtplib do?

A) Email client
B) Send emails via SMTP protocol
C) Read emails
D) Email validation

**Answer: B**

**Explanation:**
```python
with smtplib.SMTP('smtp.gmail.com', 587) as s:
    s.starttls()
    s.login(user, password)
    s.send_message(msg)
```
SMTP for sending. Use `email` module to build message. For reading: `imaplib` (IMAP) or `poplib` (POP3).

---

**Q18.46: Intermediate - [FTP with ftplib]**

What does ftplib provide?

A) File transfer
B) FTP client for file upload/download
C) Web browsing
D) Secure transfer only

**Answer: B**

**Explanation:**
`ftp = FTP('host'); ftp.login(); ftp.retrbinary('RETR file', callback)`. Upload: `storbinary`. List: `nlst()`. ⚠️ FTP is unencrypted — use SFTP (`paramiko`) or FTPS for security.

---

**Q18.47: Intermediate - [Async DNS]**

How to do async DNS lookups?

A) socket.getaddrinfo is already async
B) Use aiodns library with asyncio
C) DNS is always blocking
D) Built into aiohttp

**Answer: B**

**Explanation:**
Standard socket DNS is blocking. `aiodns` or `asyncresolver` for async DNS. aiohttp can use custom resolver. Important for high-concurrency async applications where blocking DNS is bottleneck.

---

**Q18.48: Intermediate - [Connection Timeout vs Read Timeout]**

What's the difference in `timeout=(connect, read)`?

A) No difference
B) Connect: time to establish connection; Read: time to receive data
C) Connect: first byte; Read: full response
D) Same timeout applied twice

**Answer: B**

**Explanation:**
`timeout=(3, 10)`: 3 seconds to connect, 10 seconds to read. Slow servers: connection ok but response slow. Unreachable: connection fails fast. Separate timeouts for different scenarios.

---

**Q18.49: Intermediate - [GraphQL vs REST]**

How does GraphQL differ from REST?

A) Same thing
B) GraphQL: single endpoint, client specifies exact data needed
C) REST is newer
D) GraphQL is faster always

**Answer: B**

**Explanation:**
REST: multiple endpoints, fixed response structure. GraphQL: one endpoint, query specifies fields. Avoids over/under-fetching. POST with query body. Libraries: `gql`, `sgqlc` for Python clients.

---

**Q18.50: Intermediate - [httpbin.org]**

What is httpbin.org useful for?

A) Production API
B) Testing HTTP clients — echoes back request details
C) Web hosting
D) HTTP documentation

**Answer: B**

**Explanation:**
httpbin.org: echo service for testing. `GET /get` returns request info. `POST /post` echoes body. `/status/404` returns 404. `/delay/3` delays 3 seconds. Perfect for testing HTTP code.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 4 | 8% |
| Intermediate | 46 | 92% |
| Advanced | 0 | 0% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- Socket programming basics
- urllib and requests library
- HTTP methods and status codes
- JSON APIs
- Authentication (Basic, Bearer, OAuth)
- Sessions and connection handling
- Async HTTP with aiohttp
- Error handling and timeouts
- WebSocket basics
- REST API patterns
