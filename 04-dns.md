
---

# 🌐 Day-4: DNS (Domain Name System)

## 📌 What is DNS?

DNS is like the **phonebook of the internet**. It translates human-readable domain names (like `google.com`) into IP addresses (like `142.250.185.46`) that computers use.

DNS (Domain Name System) is a **hierarchical, distributed database system** that translates domain names into IP addresses and vice versa.

Without DNS, we would need to remember IP addresses for every website we want to visit. 

---

## ❓ Why DNS Was Created

### 🚨 Problem Before DNS (pre-1983)

* Used a single file: `HOSTS.TXT`
* Maintained by Stanford Research Institute
* Downloaded by all systems

### ⚠️ Issues

* File became too large
* Frequent updates
* Network congestion
* No scalability
* No uniqueness guarantee

---

### ✅ DNS Solution

* Distributed → No single point of failure
* Hierarchical → Organized structure
* Cached → Faster responses
* Scalable → Handles billions of queries
* Delegated → Managed by multiple organizations

---

## ⚙️ How DNS Works (Basic Flow)

1. You type `www.example.com` in browser
2. Browser asks DNS resolver
3. Resolver checks cache
4. If not found → queries:

   * Root server
   * TLD server
   * Authoritative server
5. Gets IP (e.g., `93.184.216.34`)
6. Browser connects to server

---

## 🌳 DNS Hierarchy

```
                        . (Root)
                         |
        ┌────────────────┼────────────────┐
       .com            .org             .net
        |
    example.com
        |
   ┌────┴────┐
  www      api
```

---

## 📚 Types of DNS Records

| Record | Purpose       | Example                     |
| ------ | ------------- | --------------------------- |
| A      | Domain → IPv4 | example.com → 93.184.216.34 |
| AAAA   | Domain → IPv6 | example.com → IPv6          |
| CNAME  | Alias         | www → example.com           |
| MX     | Mail server   | mail.example.com            |
| TXT    | Verification  | SPF, domain verify          |
| NS     | Nameserver    | DNS servers                 |
| PTR    | Reverse DNS   | IP → domain                 |

---

## 🌍 Real-World Examples

### 1. Basic Website

```
example.com       A       93.184.216.34
www.example.com   CNAME   example.com
```

---

### 2. Load Balancing

```
example.com   A   10.0.1.5
example.com   A   10.0.1.6
example.com   A   10.0.1.7
```

👉 DNS returns multiple IPs (Round-robin)

---

### 3. Microservices

```
api.example.com     → backend
admin.example.com   → admin panel
cdn.example.com     → CDN
```

---

## 🔍 DNS Resolution (Detailed)

### Step-by-Step:

1. Browser cache check
2. OS cache check
3. Query to DNS resolver
4. Resolver queries:

   * Root server
   * TLD server
   * Authoritative server
5. IP returned
6. Browser connects

---

## 🔁 Types of DNS Queries

### 1. Recursive Query

* Client asks resolver for final answer

### 2. Iterative Query

* Resolver asks multiple servers

### 3. Non-Recursive Query

* Server already has answer

---

## ⚡ DNS Caching

### Cache Levels:

1. Browser
2. Operating System
3. Router
4. ISP Resolver
5. DNS Servers

---

## ⏱️ TTL (Time To Live)

```
example.com   300   A   93.184.216.34
```

* 300 seconds = 5 minutes

### TTL Strategy

| Type     | Use Case       |
| -------- | -------------- |
| High TTL | Stable systems |
| Low TTL  | Deployments    |

### Best Practice (Migration)

1. Reduce TTL (before change)
2. Apply changes
3. Increase TTL later

---

## ❌ Negative Caching

* Stores failed queries (NXDOMAIN)
* Prevents repeated unnecessary queries

---

## 🛠️ Common DNS Commands

```bash
# Basic lookup
nslookup example.com

# Detailed query
dig example.com

# Specific record
dig example.com MX

# Query DNS server
dig @8.8.8.8 example.com

# Reverse lookup
dig -x 8.8.8.8
```

---

## 🌐 Public DNS Servers

| Provider   | Primary        | Secondary      |
| ---------- | -------------- | -------------- |
| Google     | 8.8.8.8        | 8.8.4.4        |
| Cloudflare | 1.1.1.1        | 1.0.0.1        |
| OpenDNS    | 208.67.222.222 | 208.67.220.220 |

---

## 🚀 DNS in DevOps

### 1. Internal DNS

```
database.internal → 10.0.2.15
redis.internal    → 10.0.2.20
```

---

### 2. Kubernetes DNS

```
service.namespace.svc.cluster.local
```

---

### 3. Blue-Green Deployment

```
Before: api → old server
After:  api → new server
```

---

### 4. Cloud DNS (AWS Route53)

* Weighted routing
* Failover
* Geo routing
* Latency routing

---

## ⚠️ Common DNS Issues

### 1. DNS Propagation Delay

* Can take up to 48 hours

### 2. Cache Poisoning

* Fixed using DNSSEC

### 3. Wrong Records

```bash
dig your-domain.com
ipconfig /flushdns
```

---

## 🧠 Key Takeaways

* DNS converts domain → IP
* A = IPv4, AAAA = IPv6
* CNAME = alias
* TTL controls caching
* Critical for DevOps & Microservices
* Always test DNS changes

---

# 🔥 Extra Additions (DevOps Focus)

👉 You can optionally add:

* DNS + Load Balancer relation
* CDN (Cloudflare, Akamai)
* DNS Failover architecture
* Interview questions section


