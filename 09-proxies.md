

---

# Proxies & Reverse Proxies ( Day-9)

## What is a Proxy?

A proxy is an intermediary server that sits between clients and servers, forwarding requests and responses.

---

## The Proxy Concept

At its core, a proxy is a middleman:

### Without Proxy:

```
Client ←------ Direct Connection ------→ Server
```

### With Proxy:

```
Client ←--→ Proxy ←--→ Server
```

---

## Why Use a Middleman?

Control: Proxy can inspect, modify, or block traffic
Caching: Proxy can store responses for faster access
Security: Proxy can filter malicious content
Anonymity: Hide client or server identity
Load Distribution: Distribute requests across servers

---

## Proxy vs Gateway vs Intermediary

### Terminology:

Proxy: Generic term for intermediary
Forward Proxy: Sits in front of clients
Reverse Proxy: Sits in front of servers
Gateway: Can modify protocol (HTTP to HTTPS)
Tunnel: Passes data without understanding it

---

## Forward Proxy vs Reverse Proxy

The key difference is who it serves and where it sits.

---

## Forward Proxy (Regular Proxy)

Sits in front of clients, makes requests on their behalf.

### Position in Network:

```
Client (You) → Forward Proxy → Internet → Server
```

### Client perspective:

Proxy represents the server

### Server perspective:

Proxy IS the client

---

### What Happens:

1. Client wants to access google.com
2. Client asks Forward Proxy: "Get me google.com"
3. Forward Proxy: Makes request to google.com
4. Forward Proxy: Receives response
5. Forward Proxy: Returns response to client

---

From google.com's view: Request came from proxy, not client

Who Controls It: Client's organization (company, ISP, user)

---

## Purpose from Client's Perspective:

Access control (block certain websites)
Content filtering (block malware, adult content)
Privacy (hide real IP address)
Bypass geo-restrictions
Caching (faster access to frequently visited sites)
Bandwidth monitoring

---

## Corporate Forward Proxy Example:

```
Employee Computer → Corporate Proxy → Internet
```

Proxy Rules:

* Block social media during work hours
* Block malware/phishing sites
* Log all internet activity
* Cache common downloads
* Enforce acceptable use policy

---

## Anonymous Forward Proxy Example:

```
Your Computer (IP: 203.0.113.5)
       ↓
Forward Proxy (IP: 198.51.100.10)
       ↓
Website
```

Website logs: Request from 198.51.100.10 (not your real IP)
ISP sees: Connection to proxy (not final destination)

---

## Reverse Proxy

Sits in front of servers, receives requests on their behalf.

### Position in Network:

```
Client → Internet → Reverse Proxy → Backend Server
```

### Client perspective:

Reverse proxy IS the server

### Server perspective:

Proxy represents the client

---

## What Happens:

1. Client wants to access example.com
2. DNS resolves example.com to Reverse Proxy IP
3. Client connects to Reverse Proxy
4. Reverse Proxy: Receives request
5. Reverse Proxy: Forwards to appropriate backend server
6. Backend: Processes request
7. Reverse Proxy: Returns response to client

---

From client's view: Talked to example.com
Reality: Talked to reverse proxy, which talked to backend

Who Controls It: Server's organization (website owner, company)

---

## Purpose from Server's Perspective:

Load balancing (distribute traffic across servers)
SSL termination (handle encryption once, not per server)
Caching (reduce backend load)
Security (hide backend topology, WAF, DDoS protection)
Compression (compress responses once)
Single entry point (one IP for multiple services)

---

## Reverse Proxy Architecture:

```
Internet (Clients)
       ↓
Reverse Proxy (203.0.113.10) ← Only IP clients know
       ↓
    ┌──┴──┬───────┬────────┐
    ↓     ↓       ↓        ↓
Server1 Server2 Server3 Server4 (Private IPs: 10.0.1.x)
(API)   (API)   (Web)   (Web)
```

Clients can't directly access backend servers
All traffic goes through reverse proxy

---

## Key Differences

| Aspect        | Forward Proxy           | Reverse Proxy              |
| ------------- | ----------------------- | -------------------------- |
| Serves        | Clients                 | Servers                    |
| Position      | Client-side             | Server-side                |
| Controlled By | Client's org            | Server's org               |
| Hides         | Client identity         | Server identity            |
| Client Knows? | Yes (configured)        | No (transparent)           |
| Purpose       | Access control, privacy | Load balancing, security   |
| Configuration | Client-side             | Server-side                |
| Examples      | Squid, corporate proxy  | Nginx, HAProxy, Cloudflare |

---

## Transparent vs Explicit Proxy

### Explicit (Non-Transparent) Proxy:

Client configuration:

* Proxy: proxy.company.com:8080
* Username: john
* Password: secret

Client knows about proxy and explicitly configured to use it

---

### Transparent Proxy:

Network configuration:

* Router intercepts all HTTP traffic
* Redirects to proxy without client knowing

Client thinks: Direct connection to internet
Reality: All traffic goes through proxy

---

## How Transparent Proxy Works:

1. Client sends packet: 203.0.113.5 → 93.184.216.34:80
2. Router intercepts at firewall
3. Router redirects to: proxy.internal:3128
4. Proxy processes and forwards
5. Proxy returns response as if from original server

Client never configured proxy - it's invisible

---

## Proxy Chain

```
Client → Proxy 1 → Proxy 2 → Proxy 3 → Server
```

Each proxy only knows:

* Previous hop
* Next hop

Result: Maximum anonymity (Tor uses this concept)

---

## Key Takeaways

* Forward proxy sits in front of clients (client-side)
* Reverse proxy sits in front of servers (server-side)
* Reverse proxies handle: load balancing, SSL termination, caching
* Nginx is the most popular reverse proxy
* Always forward X-Real-IP and X-Forwarded-For headers
* Caching at proxy level reduces backend load
* Proxies provide single entry point for multiple services
* Use reverse proxies for security and traffic management

---

