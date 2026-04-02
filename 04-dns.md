

---

# 🌐 DNS (Domain Name System) ( Day-4)

## What is DNS?

DNS is like the phonebook of the internet. It translates human-readable domain names (like google.com) into IP addresses (like 142.250.185.46) that computers use.

DNS (Domain Name System) is a hierarchical, distributed database system that translates domain names into IP addresses and vice versa. Without DNS, we would need to remember IP addresses for every website we want to visit. 

---

# Why DNS Was Created

## The Problem Before DNS (pre-1983):

HOSTS.TXT file: A single text file maintained by Stanford Research Institute
Downloaded periodically by all hosts on the internet
Contained all hostname-to-IP mappings

As internet grew, this became unsustainable:

* File became too large
* Updates too frequent
* Network congestion from downloads
* No name uniqueness guarantee
* No scalability

---

## The DNS Solution:

* Distributed: No single point of failure
* Hierarchical: Organized tree structure
* Cached: Faster responses, reduced load
* Scalable: Can handle billions of queries
* Delegated: Different organizations manage different parts

---

# How DNS Fundamentally Works

DNS operates on a query-response model:

Application needs IP: Browser wants to visit example.com
Query sent to resolver: "What's the IP for example.com?"
Resolver checks cache: Recently looked up?
If not cached, recursive resolution begins
IP returned to application
Result cached for future use

---

# DNS as a Distributed Database

DNS is not a single server but millions of servers worldwide:

Root servers: 13 root server clusters (hundreds of actual servers)
TLD servers: Servers for .com, .org, .net, etc.
Authoritative servers: Servers that know specific domains
Recursive resolvers: Servers that do the lookup work for clients

This distribution provides:

* Redundancy: No single point of failure
* Performance: Queries answered locally when possible
* Scalability: Load distributed across many servers

---

# How DNS Works (Simple Flow)

1. You type: [www.example.com](http://www.example.com) in browser
2. Browser asks DNS resolver: "What's the IP for example.com?"
3. DNS resolver checks its cache
4. If not cached, resolver asks root servers → TLD servers → authoritative server
5. Gets IP: 93.184.216.34
6. Browser connects to that IP

---

# DNS Hierarchy

```id="8hh0rl"
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

# Types of DNS Records

| Record Type | Purpose                          | Example                                                 |
| ----------- | -------------------------------- | ------------------------------------------------------- |
| A           | Maps domain to IPv4              | example.com → 93.184.216.34                             |
| AAAA        | Maps domain to IPv6              | example.com → 2606:2800:220:1:248:1893:25c8:1946        |
| CNAME       | Alias to another domain          | [www.example.com](http://www.example.com) → example.com |
| MX          | Mail server                      | example.com → mail.example.com                          |
| TXT         | Text records (verification, SPF) | Used for domain verification                            |
| NS          | Nameserver records               | Points to DNS servers                                   |
| PTR         | Reverse DNS (IP to domain)       | 34.216.184.93 → example.com                             |

---

# Real-World Examples

## Example 1: Basic Website Setup

example.com.        A       93.184.216.34
[www.example.com](http://www.example.com).    CNAME   example.com.

Both example.com and [www.example.com](http://www.example.com) point to the same server.

---

## Example 2: Load Balanced Application

example.com.    A    10.0.1.5
example.com.    A    10.0.1.6
example.com.    A    10.0.1.7

DNS returns all IPs (Round-robin DNS load balancing).

---

## Example 3: Microservices in Cloud

api.example.com      A       54.123.45.67
admin.example.com    A       54.123.45.68
cdn.example.com      CNAME   d111111abcdef8.cloudfront.net

---

# DNS Resolution Process (Detailed)

## The Complete Journey of a DNS Query

When you type [www.example.com](http://www.example.com) in your browser, here's the detailed process:

---

### Step 1: Browser Cache Check

Browser: "Do I already know example.com's IP?"
Cache: "Yes, it's 93.184.216.34" → DONE (fastest)

OR

Cache: "No, I don't have it" → Continue to Step 2

---

### Step 2: Operating System Cache

OS: "Do I have example.com cached?"
Cache: "Yes, here's the IP" → DONE

OR

Cache: "No" → Continue to Step 3

---

### Step 3: Recursive Resolver Query

Your computer → Recursive Resolver (usually your ISP or 8.8.8.8)
"What's the IP for [www.example.com](http://www.example.com)?"

---

### Step 4: Recursive Resolution Begins

---

#### Step 4a: Query Root Server

Resolver → Root Server: "Where can I find .com?"
Root Server → Resolver: "Ask the .com TLD servers at these IPs"

---

#### Step 4b: Query TLD Server

Resolver → .com TLD Server: "Where can I find example.com?"
TLD Server → Resolver: "Ask example.com's nameservers at these IPs"

---

#### Step 4c: Query Authoritative Server

Resolver → example.com Nameserver: "What's [www.example.com](http://www.example.com)?"
Authoritative Server → Resolver: "It's 93.184.216.34"

---

#### Step 4d: Return to Client

Resolver → Your Computer: "[www.example.com](http://www.example.com) is 93.184.216.34"

Resolver also caches this for future queries

---

### Step 5: Connection

Browser now connects to 93.184.216.34

---

# Types of DNS Queries

## 1. Recursive Query

Client → Resolver: "Give me the answer or an error"

---

## 2. Iterative Query

Resolver → Server: "What do you know about example.com?"

---

## 3. Non-Recursive Query

Resolver → Server: "What's example.com?"

---

# DNS Query Types

A record query: "What's the IPv4 address?"
AAAA record query: "What's the IPv6 address?"
MX record query: "Where should I send mail?"
NS record query: "Who are the nameservers?"
ANY query: "Give me all records" (often blocked now)

---

# DNS Caching

DNS responses are cached at multiple levels to improve performance and reduce load on DNS infrastructure.

---

## Cache Hierarchy (Top to Bottom):

1. Browser Cache
2. Operating System Cache
3. Router Cache
4. ISP Recursive Resolver Cache
5. Intermediate DNS Server Caches

---

# TTL (Time To Live)

```id="m7s2l2"
example.com.    300    A    93.184.216.34
```

TTL in seconds (5 minutes)

---

# Negative Caching

DNS also caches negative responses (NXDOMAIN - domain doesn't exist)

---

# Common DNS Commands

```bash id="k2p7ij"
nslookup example.com
dig example.com
dig example.com MX
dig @8.8.8.8 example.com
dig -x 8.8.8.8
```

---

# Public DNS Servers

| Provider   | Primary        | Secondary      |
| ---------- | -------------- | -------------- |
| Google     | 8.8.8.8        | 8.8.4.4        |
| Cloudflare | 1.1.1.1        | 1.0.0.1        |
| OpenDNS    | 208.67.222.222 | 208.67.220.220 |

---

# DNS in DevOps

## 1. Internal DNS (Private)

database.internal → 10.0.2.15
redis.internal → 10.0.2.20
api.internal → 10.0.1.10

---

## 2. Service Discovery

my-service.default.svc.cluster.local → 10.96.0.10

---

## 3. Blue-Green Deployments

api.example.com → 1.2.3.4
api.example.com → 5.6.7.8

---

## 4. Route53 / Cloud DNS

Weighted routing
Geolocation routing
Failover routing
Latency-based routing

---

# Common DNS Issues

## DNS Propagation Delay

After updating DNS, changes take time (up to 48 hours globally)

---

## DNS Cache Poisoning

Attackers inject fake DNS records

---

## Wrong DNS Records

```bash id="p7e9r3"
dig your-domain.com
ipconfig /flushdns
```

---

# DNS Resolution Example

Query: [www.shop.example.com](http://www.shop.example.com)

1. Browser cache: Not found
2. OS cache: Not found
3. Router cache: Not found
4. ISP Resolver: Not found
5. Root server: "Go ask .com"
6. .com TLD: "Go ask example.com nameservers"
7. example.com NS: "shop.example.com is at 10.0.1.5"
8. Returns: 10.0.1.5
9. Browser connects to 10.0.1.5

---

# Key Takeaways

* DNS translates domain names to IP addresses
* A records point to IPv4, AAAA to IPv6
* CNAME creates aliases
* TTL controls caching duration
* DNS is critical for service discovery in microservices
* Always test DNS changes before going live
* Use dig or nslookup for troubleshooting

---

