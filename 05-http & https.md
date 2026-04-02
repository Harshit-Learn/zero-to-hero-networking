

---

# 🌐 Day-5: HTTP / HTTPS & Web Protocols

## 📌 What is HTTP?

HTTP (HyperText Transfer Protocol) is the **foundation of data communication on the web**. It defines how clients (browsers) and servers communicate.

* Application-layer protocol
* Invented by Tim Berners-Lee (1989)
* Works on **request-response model**

Without HTTP, browsers and servers cannot communicate. 

---

## ⚙️ Core Characteristics

### 1️⃣ Client-Server Model

```
Client (Browser / App)  ←→  Server (Web / API)
```

---

### 2️⃣ Request-Response

* Client sends request
* Server returns response

---

### 3️⃣ Stateless Protocol

HTTP **does not remember previous requests**

👉 Example:

```
GET /page1 → Response  
GET /page2 → No memory of page1
```

### 🔧 How State is Managed:

* Cookies
* Sessions
* Tokens (JWT, OAuth)
* Local Storage

---

### 4️⃣ Text-Based Protocol

HTTP/1.x is human-readable:

```
GET /index.html HTTP/1.1
Host: example.com
```

---

## 🔄 How HTTP Works (Flow)

1. DNS resolves domain → IP
2. TCP connection established
3. Client sends HTTP request
4. Server processes request
5. Server sends response
6. Connection closed or reused

---

## 🔐 HTTP vs HTTPS

| Feature  | HTTP            | HTTPS             |
| -------- | --------------- | ----------------- |
| Port     | 80              | 443               |
| Security | ❌ No encryption | ✅ Encrypted (TLS) |
| Usage    | Development     | Production        |

👉 Rule: **Always use HTTPS**

---

## 🔁 Request-Response Example

```
Client → Server:
GET /api/users HTTP/1.1

Server → Client:
HTTP/1.1 200 OK
{ "users": [...] }
```

---

## 📚 HTTP Methods

| Method  | Purpose         |
| ------- | --------------- |
| GET     | Fetch data      |
| POST    | Create          |
| PUT     | Update full     |
| PATCH   | Update partial  |
| DELETE  | Remove          |
| HEAD    | Headers only    |
| OPTIONS | Allowed methods |

---

## 📊 HTTP Status Codes

### ✅ 2xx (Success)

* 200 OK
* 201 Created
* 204 No Content

### 🔁 3xx (Redirect)

* 301 Permanent
* 302 Temporary
* 304 Not Modified

### ❌ 4xx (Client Error)

* 400 Bad Request
* 401 Unauthorized
* 403 Forbidden
* 404 Not Found
* 429 Too Many Requests

### 💥 5xx (Server Error)

* 500 Internal Error
* 502 Bad Gateway
* 503 Service Unavailable
* 504 Timeout

---

## 📦 HTTP Request Structure

```
GET /api/users HTTP/1.1
Host: api.example.com
Authorization: Bearer token

{
  "name": "John"
}
```

---

## 📦 HTTP Response Structure

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "John"
}
```

---

## 🧠 Important Headers

### Request Headers

* Host
* Authorization
* Content-Type
* Cookie

### Response Headers

* Content-Type
* Cache-Control
* Set-Cookie
* CORS headers

---

# 🔐 HTTPS & TLS

## 📌 What is HTTPS?

HTTPS = HTTP + TLS (Encryption)

---

## 🤝 TLS Handshake Process

1. Client Hello
2. Server Hello
3. Certificate Verification
4. Key Exchange
5. Session Key Generated
6. Secure Communication

---

## 📜 SSL Certificate

* Proves server identity
* Contains public key
* Signed by CA

### Types:

* DV (Free, basic)
* OV (Organization verified)
* EV (High trust)

---

## ⚡ HTTP Versions

### 🧱 HTTP/1.0

* One request per connection

---

### 🔄 HTTP/1.1

* Keep-alive
* Persistent connections

---

### 🚀 HTTP/2

* Multiplexing
* Binary protocol
* Header compression

---

### ⚡ HTTP/3

* Uses QUIC (UDP)
* Faster + no head-of-line blocking

---

## 🚀 DevOps Use Cases

### 1️⃣ API Gateway

```
Client → HTTPS → Gateway → HTTP → Backend
```

---

### 2️⃣ Load Balancer

```
Client → HTTPS → LB → HTTP → Servers
```

👉 SSL termination happens at Load Balancer

---

### 3️⃣ Health Check

```
GET /health → 200 OK
```

---

## 🛠️ Useful Commands

```bash
# GET request
curl https://api.example.com

# POST request
curl -X POST -H "Content-Type: application/json" -d '{"name":"John"}'

# Debug request
curl -v https://example.com
```

---

## 🔐 SSL Debugging

```bash
openssl s_client -connect example.com:443
```

---

## 🔄 REST API Convention

```
GET    /users
POST   /users
PUT    /users/1
PATCH  /users/1
DELETE /users/1
```

---

## 🌍 CORS

Allows cross-domain requests:

```
Access-Control-Allow-Origin: *
```

---

## ⚡ Caching

### Cache-Control

```
Cache-Control: max-age=3600
```

### ETag

* Helps avoid re-downloading data

---

## 🔌 WebSockets

* Real-time communication
* Bidirectional

Use cases:

* Chat apps
* Live dashboards

---

## ⚠️ Common Issues

### 502 Error

```
Check backend service
```

---

### SSL Error

```
openssl s_client -connect example.com:443
```

---

### CORS Error

Add headers:

```
Access-Control-Allow-Origin: *
```

---

## 🧠 Key Takeaways

* HTTP is stateless
* HTTPS is secure
* Status codes matter
* Headers carry metadata
* REST uses HTTP methods
* curl is essential for debugging

---


