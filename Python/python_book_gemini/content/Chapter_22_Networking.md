# Chapter 22: Networking & Internet

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `urllib.request` vs `requests`, `socket` programming (TCP/UDP), HTTP protocols (GET/POST, Headers, Status Codes), JSON APIs, `ipaddress` module, `http.server`, `http.client`, DNS basics (`socket.gethostbyname`), Port numbers, Timeout handling, `ftplib`.

---

**Q22.1: Basic - [Requests Module]**

The most popular third-party library for making HTTP requests in Python (more user-friendly than `urllib`) is:

A) `http`
B) `requests`
C) `socket`
D) `fetch`

**Answer: B**

**Explanation:**
"Requests: HTTP for Humans". It simplifies common tasks like session handling, decoding, and form data.

---

**Q22.2: Intermediate - [Socket TCP]**

To create a TCP socket, you generally use:

A) `socket.socket(socket.AF_INET, socket.SOCK_STREAM)`
B) `socket.socket(socket.AF_INET, socket.SOCK_DGRAM)`
C) `socket.socket(socket.AF_UNIX, socket.SOCK_STREAM)`
D) `socket.tcp()`

**Answer: A**

**Explanation:**
`AF_INET` implies IPv4, and `SOCK_STREAM` implies TCP (Transmission Control Protocol).

---

**Q22.3: Advanced - [HTTP Status 418]**

HTTP Status Code 418 comes from an April Fools RFC and means:

A) Not Found.
B) I'm a teapot.
C) Server Error.
D) Forbidden.

**Answer: B**

**Explanation:**
The "Hyper Text Coffee Pot Control Protocol" (HTCPCP). Python's `http.HttpStatus.IM_A_TEAPOT` handles this.

---

**Q22.4: Basic - [Urllib Request]**

The standard library module to fetching a URL is:

A) `urllib.request`
B) `urllib.fetch`
C) `net.http`
D) `web.get`

**Answer: A**

**Explanation:**
Standard mechanism since Python 3, replacing Python 2's `urllib2`.

---

**Q22.5: Intermediate - [JSON Response]**

When using `requests`, `response.json()`:

A) Validates XML.
B) Decodes the response content (assumed JSON) into a Python dictionary/list.
C) Returns raw text.
D) Saves to file.

**Answer: B**

**Explanation:**
It calls `json.loads()` on the text content, raising `JSONDecodeError` if invalid.

---

**Q22.6: Advanced - [Socket Listen]**

`socket.listen(5)` argument (5) specifies:

A) The timeout.
B) The backlog (number of unaccepted connections that the system will allow before refusing new ones).
C) The port number.
D) The number of threads.

**Answer: B**

**Explanation:**
Controls the size of the queue for pending connections.

---

**Q22.7: Basic - [Localhost IP]**

The standard loopback IP address for localhost (IPv4) is:

A) 192.168.1.1
B) 10.0.0.1
C) 127.0.0.1
D) 0.0.0.0

**Answer: C**

**Explanation:**
Refers to the local machine.

---

**Q22.8: Intermediate - [UDP Socket]**

UDP (User Datagram Protocol) is:

A) Connection-oriented and reliable.
B) Connectionless and unreliable (best effort), but faster.
C) Encrypted.
D) For huge files only.

**Answer: B**

**Explanation:**
Used for real-time applications (VoIP, Games) where dropping a packet is better than waiting for retransmission. Use `SOCK_DGRAM`.

---

**Q22.9: Advanced - [Ipaddress Module]**

`ipaddress.ip_network('192.168.0.0/28').num_addresses` is:

A) 256
B) 16
C) 32
D) 14

**Answer: B**

**Explanation:**
A /28 subnet mask leaves 4 bits for hosts. 2^4 = 16.

---

**Q22.10: Expert - [Socket Bind]**

To start a server on "all interfaces" (publicly accessible), you bind to:

A) `127.0.0.1`
B) `localhost`
C) `0.0.0.0` (or empty string `''`)
D) `255.255.255.255`

**Answer: C**

**Explanation:**
INADDR_ANY. Binding to `127.0.0.1` only allows local connections.

---

**Q22.11: Basic - [Port 80]**

Standard port for unencrypted Web traffic (HTTP) is:

A) 21
B) 22
C) 80
D) 443

**Answer: C**

**Explanation:**
Port 443 is HTTPS. 22 is SSH. 21 is FTP.

---

**Q22.12: Intermediate - [Requests Session]**

Using `s = requests.Session()`:

A) Persists parameters (like cookies) across multiple requests involving the same `s` object.
B) Is meaningless.
C) Is slower.
D) Prevents cookies.

**Answer: A**

**Explanation:**
Also enables connection pooling (keep-alive), improving performance for multiple requests to the same host.

---

**Q22.13: Advanced - [IPv6 Address]**

Which is a valid IPv6 address?

A) `192.168.1.1`
B) `::1`
C) `256.0.0.1`
D) `127.0.0.1`

**Answer: B**

**Explanation:**
IPv6 uses hex notated 128-bit addresses. `::1` is localhost.

---

**Q22.14: Basic - [DNS Lookup]**

The function to convert a hostname (e.g., "google.com") to an IP address is:

A) `socket.gethostbyname()`
B) `socket.getaddr()`
C) `dns.lookup()`
D) `ip.find()`

**Answer: A**

**Explanation:**
Uses the OS resolver to perform the DNS query.

---

**Q22.15: Intermediate - [Post Data]**

In `requests.post(url, data=payload)`:

A) Form-encodes the data content type `application/x-www-form-urlencoded`.
B) Sends JSON.
C) Sends XML.
D) Fails.

**Answer: A**

**Explanation:**
To send JSON, correct usage is `requests.post(url, json=payload)` or passing `data=json.dumps(payload)` with headers manually set.

---

**Q22.16: Advanced - [Socket Timeout]**

`socket.settimeout(None)` means:

A) Blocking mode (wait forever).
B) Non-blocking (return error immediately if not ready).
C) Wait 0 seconds.
D) Wait 1 minute.

**Answer: A**

**Explanation:**
Default behavior. `settimeout(0.0)` makes it non-blocking. `settimeout(n)` blocks for n seconds.

---

**Q22.17: Expert - [Select Module]**

The `select` module is used for:

A) Selecting database rows.
B) Multiplexing I/O (monitoring multiple sockets/files to see which are ready for reading/writing).
C) Choosing random numbers.
D) Selecting UI elements.

**Answer: B**

**Explanation:**
Essential for building concurrent network servers without threads (async I/O foundations).

---

**Q22.18: Intermediate - [FTPlib]**

The `ftplib` module implements:

A) File Transfer Protocol client.
B) File Transfer Protocol server.
C) HTTP.
D) SSH.

**Answer: A**

**Explanation:**
Allows uploading/downloading files via FTP.

---

**Q22.19: Basic - [HTTP Methods]**

Which HTTP method is idempotent and intended for retrieving data?

A) POST
B) GET
C) DELETE
D) CREATE

**Answer: B**

**Explanation:**
GET should not have side effects. POST is for submitting data.

---

**Q22.20: Advanced - [Simple HTTP Server]**

Command `python -m http.server`:

A) Starts a basic web server serving files from the current directory.
B) Hacks the network.
C) Downloads the internet.
D) Checks connection.

**Answer: A**

**Explanation:**
Handy utility for quick file sharing or testing static sites.

---

**Q22.21: Expert - [GIL Socket]**

Does the Python GIL prevent concurrent network I/O?

A) Yes, heavily.
B) No. The GIL is released during I/O operations (like `socket.recv`), allowing other threads to run while one waits for network data.
C) Yes, only one socket works at a time.
D) Sockets don't use the CPU.

**Answer: B**

**Explanation:**
Network I/O is one area where Python threading is actually effective because threads spend most time sleeping/waiting.

---

**Q22.22: Intermediate - [Urlparse]**

`urllib.parse.urlparse("http://site.com:80/foo?q=1")`:

A) Downloads the page.
B) Parses the URL strings into components (scheme, netloc, path, query, etc.).
C) Validates the site is online.
D) Returns IP.

**Answer: B**

**Explanation:**
Useful for manipulating or extracting parts of a URL.

---

**Q22.23: Basic - [Ping]**

"Ping" typically uses which protocol (in `subprocess` usually, since raw sockets require root)?

A) TCP
B) UDP
C) ICMP
D) HTTP

**Answer: C**

**Explanation:**
Internet Control Message Protocol.

---

**Q22.24: Advanced - [SSL Handshake]**

`ssl.wrap_socket` (or `context.wrap_socket`) performs:

A) Encryption of the Python script.
B) The TLS/SSL handshake to establish an encrypted connection over a raw socket.
C) Wrapping the socket in foil.
D) Closing the socket.

**Answer: B**

**Explanation:**
Upgrades a plain TCP connection to a secure one.

---

**Q22.25: Intermediate - [Requests Raise For Status]**

`response.raise_for_status()` will:

A) Raise an exception (HTTPError) if the status code was 4xx or 5xx.
B) Print the status code.
C) Raise status level.
D) Do nothing.

**Answer: A**

**Explanation:**
Best practice to ensure you don't silently ignore failed requests.

---

**Q22.26: Expert - [Nagle Algorithm]**

Socket option `TCP_NODELAY` disables Nagle's algorithm. This is desirable when:

A) Sending large files.
B) Improving latency for small, frequent messages (like SSH or real-time games).
C) Reducing bandwidth.
D) Increasing throughput.

**Answer: B**

**Explanation:**
Nagle buffers small packets to combine them, which saves bandwidth but hurts latency.

---

**Q22.27: Basic - [Download File]**

Basic way to save a binary file from a response:

A) `f.write(r.text)`
B) `f.write(r.content)` (in 'wb' mode).
C) `f.save(r)`
D) `r.save(f)`

**Answer: B**

**Explanation:**
`content` gives raw bytes. `text` tries to decode as unicode.

---

**Q22.28: Advanced - [Cookie Jar]**

In `http.cookiejar`, a `CookieJar` object:

A) Stores cookies in memory for HTTP requests.
B) Bakes cookies.
C) Is a browser.
D) Is a server.

**Answer: A**

**Explanation:**
Used by `urllib` openers to handle state.

---

**Q22.29: Intermediate - [User Agent]**

A "User-Agent" header generally identifies:

A) The user's name.
B) The client software (browser/script) making the request.
C) The OS only.
D) The IP address.

**Answer: B**

**Explanation:**
Many servers block requests with the default generic Python user-agent, so spoofing it is common.

---

**Q22.30: Expert - [Epoll]**

On Linux, `select.epoll()`:

A) Is a slower version of select.
B) Is a scalable I/O event notification mechanism (O(1)), far more efficient than `select` (O(N)) for thousands of connections.
C) Is for polling emails.
D) Is Windows only.

**Answer: B**

**Explanation:**
The underlying mechanism for high-performance python async servers (like nginx proxies).

---

**Q22.31: Intermediate - [Socket Shutdown]**

`socket.shutdown(how)` is used to:

A) Close the socket completely (release file descriptor).
B) Disable further sends and/or receives, sending a standardized "End of File" (FIN) signal to the peer.
C) Turn off the computer.
D) Pause the socket.

**Answer: B**

**Explanation:**
Distinct from `close()`. `shutdown(SHUT_WR)` tells the other side "I am done writing, but I might still listen to your response".

---

**Q22.32: Advanced - [Asyncio Networking]**

`asyncio.open_connection()` returns:

A) A raw socket.
B) A tuple `(reader, writer)` streams.
C) A Future.
D) A coroutine.

**Answer: B**

**Explanation:**
High-level stream API for managing TCP connections in asyncio.

---

**Q22.33: Basic - [Port Range]**

Valid port numbers (unsigned 16-bit integer) range from:

A) 0 to 65535
B) 1 to 1000
C) 0 to 255
D) -1 to 10000

**Answer: A**

**Explanation:**
Network ports are 16-bit fields.

---

**Q22.34: Expert - [SO_REUSEADDR]**

Setting `linesocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)` allows:

A) Multiple sockets to bind to the same IP/Port immediately after one closes (bypassing TIME_WAIT state).
B) Reusing the address for different protocols.
C) Hacking IP.
D) Speed boost.

**Answer: A**

**Explanation:**
Essential for server development; prevents "Address already in use" errors when restarting a server quickly.

---

**Q22.35: Intermediate - [Requests Chunked]**

`requests.get(url, stream=True)` allows:

A) Viewing videos.
B) Consuming response data in chunks (iterator) instead of loading the entire body into memory at once.
C) Faster download.
D) Streaming music.

**Answer: B**

**Explanation:**
Critical for downloading large files (> RAM size).

---

**Q22.36: Advanced - [HTTP Head]**

An HTTP HEAD request differs from GET in that:

A) It is faster.
B) It requests the headers ONLY, without the response body.
C) It is for authentication.
D) It gets the first 10 bytes.

**Answer: B**

**Explanation:**
Useful for checking if a resource exists or checking its Last-Modified date without downloading it.

---

**Q22.37: Basic - [Host to Network Order]**

`socket.htons()` converts a number from:

A) Host Byte Order to Network Byte Order (Big Endian).
B) Network to Host.
C) Hex to String.
D) Host to Server.

**Answer: A**

**Explanation:**
"Host to Network Short". Network protocols standardized on Big Endian; local CPUs might be Little Endian (x86).

---

**Q22.38: Intermediate - [Fake Server]**

`http.server.SimpleHTTPRequestHandler` serves files. To handle dynamic GET/POST requests, you should:

A) Edit library files.
B) Subclass `http.server.BaseHTTPRequestHandler` and override `do_GET()` / `do_POST()`.
C) Use `socket`.
D) Use regex.

**Answer: B**

**Explanation:**
The standard way to build a custom raw Python HTTP server without a framework (like Flash/Django).

---

**Q22.39: Advanced - [Socket Blocking]**

If `sock.recv(1024)` is called on a blocking socket and no data is available:

A) It returns empty bytes `b''`.
B) It returns None.
C) It pauses execution of the thread until data arrives.
D) It raises BlockingIOError.

**Answer: C**

**Explanation:**
This pause behavior is why multithreading or `select`/asyncio is needed for concurrency.

---

**Q22.40: Expert - [SSL Context check_hostname]**

When `context.check_hostname = True` (and verify_mode is CERT_REQUIRED):

A) It verifies that the certificate's subject matches the hostname you are connecting to.
B) It checks if hostname resolves.
C) It logs the hostname.
D) It does nothing.

**Answer: A**

**Explanation:**
Prevents Man-In-The-Middle (MITM) attacks where an attacker presents a valid cert for *their* domain (attacker.com) while intercepting traffic to your target (bank.com).

---

**Q22.41: Basic - [Requests Auth]**

`requests.get(url, auth=('user', 'pass'))` performs:

A) Basic Authentication.
B) Bearer Token Auth.
C) Digest Auth.
D) OAuth.

**Answer: A**

**Explanation:**
Sends the `Authorization: Basic encoded_string` header.

---

**Q22.42: Intermediate - [IPv4 Packed]**

`socket.inet_aton("127.0.0.1")` returns:

A) The integer 2130706433.
B) A 4-byte packed binary string.
C) The string "localhost".
D) An Error.

**Answer: B**

**Explanation:**
Converts the dot-decimal string to raw 32-bit network byte format.

---

**Q22.43: Advanced - [Keep Alive]**

HTTP Keep-Alive (Connection: keep-alive) benefits performance by:

A) Keeping the server awake.
B) Reusing the existing TCP connection for subsequent requests (avoiding the 3-way handshake overhead).
C) Compressing data.
D) Caching files.

**Answer: B**

**Explanation:**
Crucial for HTTPS where handshake also involves expensive crypto setup.

---

**Q22.44: Expert - [Socket Family]**

`socket.AF_UNIX` (or `AF_LOCAL`) uses:

A) TCP/IP.
B) File system paths as addresess (Unix Domain Sockets).
C) Bluetooth.
D) Satellites.

**Answer: B**

**Explanation:**
Faster than Loopback TCP for inter-process communication (IPC) on the same machine (Linux/Mac, and recently Windows 10+).

---

**Q22.45: Intermediate - [Urllib Parse Quote]**

`urllib.parse.quote("a space")`:

A) Returns `"a space"`.
B) Returns `"a%20space"`.
C) Returns `"a+space"`.
D) Errors.

**Answer: B**

**Explanation:**
URL encoding (percent encoding) for unsafe characters in URL paths.

---

**Q22.46: Basic - [Server Bind Error]**

"Address already in use" error happens when:

A) You have no internet.
B) Another process (or a lingering socket) is already bound to that specific Port.
C) The IP is wrong.
D) Firewall blocks it.

**Answer: B**

**Explanation:**
Only one socket can bind to a specific (IP, Port) combination at a time (usually).

---

**Q22.47: Advanced - [Raw Sockets]**

Creating a socket with `socket.SOCK_RAW`:

A) Allows access to transport headers (TCP/UDP) or IP headers normally mishandled by the OS kernel.
B) Sends raw meat.
C) Is easier than TCP.
D) Is Python default.

**Answer: A**

**Explanation:**
Requires Administrator/Root privileges. Used for tools like Wireshark or ping implementations.

---

**Q22.48: Expert - [Backlog Drop]**

If the listen backlog queue is full, new incoming TCP SYN packets are generally:

A) Buffered in RAM.
B) Dropped (ignored) by the kernel, causing the client to retry (TCP retransmission).
C) Charged a fee.
D) Accepted immediately.

**Answer: B**

**Explanation:**
The client eventually times out if the server never `accept()`s fast enough to drain the queue.

---

**Q22.49: Intermediate - [FTP Binary]**

When using `ftp.retrbinary('RETR filename', callback)`, transfer mode is:

A) ASCII (converts newlines).
B) Binary (exact byte copy).
C) Compressed.
D) Encrypted.

**Answer: B**

**Explanation:**
Essential for images, archives, or executables to prevent corruption from newline translation.

---

**Q22.50: Basic - [Requests Cookies]**

Cookies received in a `requests` response are available in:

A) `response.cookies` (CookieJar).
B) `response.headers`.
C) `response.text`.
D) `browser.cookies`.

**Answer: A**

**Explanation:**
Can be accessed like a dictionary.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
