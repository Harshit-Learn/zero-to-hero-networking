

---

# ⚖️ Load Balancing

## What is Load Balancing?

Load balancing distributes incoming traffic across multiple servers to ensure no single server gets overwhelmed.

Load balancing is a fundamental concept in distributed systems that solves several critical problems:

Scalability: One server has limits; multiple servers scale horizontally
Availability: If one server fails, others handle the traffic
Performance: Distributing load prevents bottlenecks
Resource Optimization: Efficiently utilize all available servers 

---

## The Core Problem:

### Without Load Balancer:

All traffic → Single Server

* Server gets 1000 req/s
* Server can handle 500 req/s
* Result: 500 req/s dropped, slow responses, server crash

---

### With Load Balancer:

Traffic → Load Balancer → Server 1 (333 req/s)
→ Server 2 (333 req/s)
→ Server 3 (333 req/s)

* Each server within capacity
* Fast responses
* System remains stable

---

# Load Balancing Theory

## Horizontal Scaling vs Vertical Scaling:

### Vertical Scaling (Scale Up):

Upgrade one server: More CPU, RAM, Disk

* Limited by hardware maximums
* Expensive
* Single point of failure
* Downtime during upgrades

---

### Horizontal Scaling (Scale Out):

Add more servers of same size

* Nearly unlimited scaling
* Cost-effective (commodity hardware)
* No single point of failure
* No downtime to add servers
* Requires load balancing

Load balancing enables horizontal scaling.

---

## Types of Load

```
                    Load Balancer
                         |
        ┌────────────────┼────────────────┐
        |                |                |
    Server 1         Server 2         Server 3
    (Active)         (Active)         (Active)
```

---

## Flow:

User sends request to load balancer
Load balancer picks a server (using an algorithm)
Request is forwarded to chosen server
Server processes and responds
Load balancer returns response to user

---

# Load Balancing Algorithms

Load balancing algorithms determine how traffic is distributed.

---

## 1. Round Robin

Distributes requests equally in sequence.

### Algorithm:

```
servers = [Server1, Server2, Server3]
current = 0

for each request:
    send to servers[current]
    current = (current + 1) % number_of_servers
```

### Example:

Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 3
Request 4 → Server 1
Request 5 → Server 2

### Advantages:

Simple to implement
Fair distribution
No overhead

### Disadvantages:

Doesn't consider server load
Doesn't consider request complexity

---

## 2. Least Connections

Sends traffic to server with fewest active connections.

### Algorithm:

```
for each request:
    find server with minimum active_connections
    send request to that server
```

### Example:

Server 1: 5 connections
Server 2: 2 connections ← chosen
Server 3: 8 connections

---

## 3. Weighted Round Robin

Servers with higher capacity get more requests.

```
Server1 → 50%
Server2 → 33%
Server3 → 17%
```

---

## 4. IP Hash

Routes same client IP to same server.

---

## 5. Least Response Time

Routes to server with fastest response time and fewest connections.

---

## 6. Random

Randomly selects a server.

---

# Types of Load Balancers

## Layer 4 (Transport Layer)

Routes based on IP address and port number

Advantages:

* Fast
* Low latency
* High throughput

Disadvantages:

* No content-based routing
* No caching
* No SSL termination

---

## Layer 7 (Application Layer)

Routes based on HTTP content

Advantages:

* Smart routing
* SSL termination
* Caching
* Security

Disadvantages:

* Slower
* More complex
* Higher cost

---

# Layer 4 vs Layer 7 Comparison

| Feature  | Layer 4  | Layer 7    |
| -------- | -------- | ---------- |
| Speed    | Fast     | Moderate   |
| Routing  | IP/Port  | URL/Header |
| SSL      | No       | Yes        |
| Use Case | TCP apps | Web apps   |

---

# Health Checks

Load balancers regularly check if servers are healthy and able to handle traffic.

---

## Types of Health Checks

### TCP Health Check

Checks TCP connection

---

### HTTP Health Check

```
GET /health → 200 OK
```

---

## Health Check Parameters

Interval
Timeout
Unhealthy Threshold
Healthy Threshold

---

# Session Persistence (Sticky Sessions)

Keep user connected to same server for entire session.

---

# Real-World Examples

## Basic Architecture

```
Internet
   ↓
Load Balancer
   ├→ Server 1
   ├→ Server 2
   └→ Server 3
```

---

## Microservices

```
/users → User Service  
/orders → Order Service  
/products → Product Service  
```

---

## Multi-Region

```
Global LB → US / EU / Asia
```

---

# Popular Load Balancers

## Software

Nginx
HAProxy
Traefik
Envoy

---

## Cloud

AWS ALB / NLB
Azure Load Balancer
GCP Load Balancing

---

## Kubernetes

Service
Ingress
Service Mesh

---

# Nginx Config

```
upstream backend {
    server 10.0.1.10:8080;
    server 10.0.1.11:8080;
    server 10.0.1.12:8080;
}

server {
    listen 80;

    location / {
        proxy_pass http://backend;
    }
}
```

---

# Load Balancing Patterns

## Active-Active

All servers handle traffic simultaneously.

## Active-Passive

One server handles traffic, others are standby.

## Geographic Load Balancing

Route users to nearest region.

---

# Auto-Scaling with Load Balancers

1. Load increases → Metrics trigger scaling
2. New servers are launched
3. Load balancer adds them to pool
4. Traffic distributed
5. Load decreases → Servers removed

---

# Common Commands & Tools

```
for i in {1..10}; do
  curl -s http://loadbalancer.example.com | grep "Server ID"
done
```

---

# Troubleshooting

## Issue: Uneven Load Distribution

Possible causes:

Sticky sessions enabled
Long-lived connections
IP hash with few clients

Solution: Change algorithm or disable sticky sessions.

---

## Issue: Server Marked Unhealthy

```
curl http://backend-server:8080/health
```

---

## Issue: 502 Bad Gateway

Possible causes:

All backend servers are down
Backend servers timing out
Network issue between LB and servers

Solution: Check backend logs and connectivity.

---

# Key Takeaways

* Load balancers distribute traffic across servers
* Round-robin is simple, least-connections adapts to load
* Layer 4 is fast, Layer 7 offers more features
* Health checks ensure traffic only goes to healthy servers
* Session persistence can cause uneven distribution
* Auto-scaling works hand-in-hand with load balancing
* Always have multiple backend servers for high availability

---
