

---

# 🌐 HTTP/HTTPS & Web Protocols ( Day-5)

## What is HTTP?

HTTP (HyperText Transfer Protocol) is the foundation of data communication on the web. It's how your browser talks to web servers.

HTTP is an application-layer protocol that defines how messages are formatted and transmitted between clients (usually web browsers) and servers. It was invented by Tim Berners-Lee in 1989 and has evolved significantly since then. 

---

# Core Characteristics of HTTP

## 1. Client-Server Model

```
Client (initiates)  ←→  Server (responds)
- Browser               - Web Server
- Mobile App            - API Server
- CLI tool (curl)       - Backend Service
```

---

## 2. Request-Response Protocol

Client sends a request
Server processes and sends a response

Each transaction is independent (unless keep-alive is used)

---

## 3. Stateless Protocol

HTTP itself has no memory of previous requests:

Request 1: GET /page1 → Server responds
Request 2: GET /page2 → Server has no memory of Request 1

Why Stateless?

Simplicity: Server doesn't need to maintain state
Scalability: Any server can handle any request
Reliability: No issues if server restarts

Problem: Web apps need state (shopping carts, login sessions)

Solutions:

Cookies: Client stores state
Sessions: Server stores state, client holds session ID
Tokens: JWT, OAuth tokens carry state
Local Storage: Client-side state

---

## 4. Text-Based Protocol (HTTP/1.x)

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
```

Note: HTTP/2 and HTTP/3 use binary format for efficiency.

---

# How HTTP Works (Request-Response Cycle)

Step 1: DNS Resolution
[www.example.com](http://www.example.com) → 93.184.216.34

Step 2: TCP Connection
Client establishes TCP connection to server:443

Step 3: HTTP Request
Client sends HTTP request over TCP connection

Step 4: Server Processing
Server processes request, accesses resources

Step 5: HTTP Response
Server sends response back to client

Step 6: Connection Handling

HTTP/1.0: Connection closes
HTTP/1.1+: Connection may stay open (keep-alive)

---

# HTTP	HTTPS

Port 80	Port 443
Unencrypted	Encrypted (TLS/SSL)
Fast	Slightly slower (encryption overhead)
Insecure	Secure
[http://example.com](http://example.com)	[https://example.com](https://example.com)

Rule of thumb: Always use HTTPS for production.

---

# How HTTP Works

```
Client                              Server
  |                                   |
  |------- HTTP Request ------------->|
  |  GET /api/users HTTP/1.1          |
  |  Host: api.example.com            |
  |                                   |
  |<------ HTTP Response -------------|
  |  HTTP/1.1 200 OK                  |
  |  Content-Type: application/json   |
  |  { "users": [...] }               |
```

---

# HTTP Methods

| Method  | Purpose                   | Example Use Case       |
| ------- | ------------------------- | ---------------------- |
| GET     | Retrieve data             | Fetch user profile     |
| POST    | Create new resource       | Register new user      |
| PUT     | Update entire resource    | Update user profile    |
| PATCH   | Partially update resource | Update user email only |
| DELETE  | Delete resource           | Delete user account    |
| HEAD    | Get headers only          | Check if file exists   |
| OPTIONS | Get allowed methods       | CORS preflight         |

---

# HTTP Status Codes

## 2xx - Success

200 OK: Request succeeded
201 Created: Resource created successfully
204 No Content: Success, but no content to return

## 3xx - Redirection

301 Moved Permanently: Resource moved (update your bookmarks)
302 Found: Temporary redirect
304 Not Modified: Use cached version

## 4xx - Client Errors

400 Bad Request: Invalid request syntax
401 Unauthorized: Authentication required
403 Forbidden: You don't have permission
404 Not Found: Resource doesn't exist
429 Too Many Requests: Rate limit exceeded

## 5xx - Server Errors

500 Internal Server Error: Server crashed
502 Bad Gateway: Gateway/proxy error
503 Service Unavailable: Server overloaded or down
504 Gateway Timeout: Gateway/proxy timeout

---

# HTTP Request Structure

```
GET /api/users/123 HTTP/1.1
Host: api.example.com
User-Agent: Mozilla/5.0
Accept: application/json
Authorization: Bearer eyJhbGc...
Content-Type: application/json

{
  "name": "John Doe"
}
```

Parts:

Request line: Method, path, version
Headers: Metadata about request
Body: Data (for POST/PUT/PATCH)

---

# HTTP Response Structure

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 156
Cache-Control: max-age=3600
Set-Cookie: sessionId=abc123

{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com"
}
```

---

# Important HTTP Headers

## Request Headers

Host: api.example.com
User-Agent: curl/7.64.1
Accept: application/json
Authorization: Bearer token123
Content-Type: application/json
Cookie: sessionId=abc123

## Response Headers

Content-Type: application/json
Content-Length: 1234
Cache-Control: max-age=3600
Set-Cookie: sessionId=xyz789
Access-Control-Allow-Origin: *
X-RateLimit-Remaining: 99

---

# HTTPS & TLS/SSL

## How HTTPS Works

HTTPS = HTTP + TLS (Transport Layer Security)

---

## The TLS Handshake Process

1. Client Hello
2. Server Hello
3. Certificate Verification
4. Key Exchange
5. Session Keys Generated
6. Encrypted Communication Begins

---

# SSL Certificates Explained

An SSL certificate is a digital document that:

Proves identity: This server is really example.com
Contains public key: Used for initial encryption
Is signed by CA: Trusted third party vouches for it

---

# HTTP Versions

## HTTP/1.0 (1996)

One request per connection

## HTTP/1.1 (1997)

Persistent connections

## HTTP/2 (2015)

Multiplexing
Binary protocol
Header compression

## HTTP/3 (2022)

Uses QUIC (UDP)

---

# Real-World DevOps Examples

## API Gateway

User → HTTPS:443 → API Gateway → HTTP:8080 → Backend Services

---

## Health Check Endpoint

```
GET /health HTTP/1.1
Host: app-service:8080
```

---

## Load Balancer Setup

Client → HTTPS:443 → Load Balancer → HTTP:8080 → App Servers

---

# Common Commands

```
curl https://api.example.com/users

curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"John","email":"john@example.com"}'
```

---

# RESTful API Conventions

```
GET    /api/users
GET    /api/users/123
POST   /api/users
PUT    /api/users/123
PATCH  /api/users/123
DELETE /api/users/123
```

---

# CORS (Cross-Origin Resource Sharing)

```
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST, OPTIONS
Access-Control-Allow-Headers: Content-Type
```

---

# Caching

```
Cache-Control: public, max-age=3600
Cache-Control: private, no-cache
Cache-Control: no-store
```

---

# WebSockets

Real-time, bidirectional communication over a single TCP connection.

---

# Common Issues & Debugging

## Issue: 502 Bad Gateway

```
curl http://localhost:8080
docker logs backend-container
```

---

## Issue: SSL Certificate Error

```
curl -k https://example.com
openssl s_client -connect example.com:443
```

---

## Issue: CORS Error

```
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST, OPTIONS
Access-Control-Allow-Headers: Content-Type
```

---

# Key Takeaways

* HTTP is stateless - each request is independent
* HTTPS encrypts traffic - always use it in production
* Status codes tell you what happened (2xx=success, 4xx=client error, 5xx=server error)
* REST APIs use HTTP methods semantically
* Headers carry metadata about requests/responses
* Understanding HTTP is crucial for debugging API issues
* Use curl for testing and debugging HTTP endpoints

---


