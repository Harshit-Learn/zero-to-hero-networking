
---

# CDN (Content Delivery Network) ( Day-10)

## What is a CDN?

A CDN is a geographically distributed network of servers that delivers content to users from the nearest location.

---

## The Distance Problem

The Fundamental Issue: Speed of light is finite, and data can't travel faster than it.

### Physics of Network Latency:

Light speed in fiber: ~200,000 km/second (2/3 speed in vacuum)

Distance: New York to Los Angeles = 4,000 km
Theoretical minimum latency: 4000 / 200000 = 0.02 seconds = 20ms

Real-world latency: 70-80ms (due to routing, switches, etc.)

---

Problem: Every round trip doubles this:

* DNS lookup: 80ms
* TCP handshake: 80ms
* TLS handshake: 80ms
* HTTP request/response: 80ms

Total: 320ms before content even loads!

---

## CDN Solution:

```id="c7s2bx"
User in Los Angeles
      ↓ 5ms latency
CDN Server in Los Angeles (has cached content)
      ↓
User gets content in 5ms instead of 80ms
```

---

## How CDN Fundamentally Works

### Architecture:

```id="y8r9hm"
                Origin Server (Your Server)
                   |
                   | Content distributed
                   |
        ┌──────────┼──────────┐
        |          |          |
    Edge PoP   Edge PoP   Edge PoP
    (New York) (London)  (Tokyo)
        |          |          |
    Caching    Caching    Caching
        |          |          |
    Users      Users      Users
```

---

## PoP (Point of Presence):

Physical location with CDN servers
Connected to local ISPs
Stores cached content
Major CDNs have 100-300+ PoPs globally

---

## CDN Request Flow (Detailed)

### First Request (Cache Miss):

1. User in London types: [www.example.com](http://www.example.com)

2. DNS Resolution:

   * Browser queries DNS
   * DNS returns: cdn-london.example.com (nearest edge)

3. User connects to London Edge Server

4. Edge Server checks cache

5. Cache Miss

6. Edge → Origin

7. Origin → Edge

8. Edge stores + returns

Total Time: 100ms (includes origin fetch)

---

### Subsequent Requests (Cache Hit):

1. Another user requests same file
2. DNS returns edge
3. Edge checks cache
4. Cache Hit
5. Response served

Total Time: 10ms

Origin Server: Not contacted at all

---

## CDN Geographic Routing

### DNS-Based Routing (Most Common):

User IP → CDN returns nearest PoP IP

Same domain, different IP based on user location

---

### Anycast Routing (Advanced):

All edge servers share same IP

Traffic automatically routed to nearest location

---

## CDN Caching Theory

### Cache Hierarchy:

Level 1: Edge Cache (closest to users)
Level 2: Regional Cache
Level 3: Origin Shield
Level 4: Origin Server

---

## Cache Eviction Policies

### LRU (Least Recently Used):

Remove least recently accessed item

### LFU (Least Frequently Used):

Remove least frequently accessed item

### TTL-Based:

Items expire after defined time

### Adaptive Algorithm:

Combines:

* Popularity
* Recency
* Size
* TTL
* Origin load

---

## CDN Cache Control

Cache-Control Header:

```id="fbb9j9"
Cache-Control: public, max-age=31536000, immutable
```

---

## Common Patterns

Static Assets: long cache
Images: daily cache
HTML: short cache
API: no cache
Sensitive: no-store

---

## Vary Header

```id="6r8y8k"
Vary: Accept-Encoding
```

Stores multiple versions based on encoding

---

## Cache Hit Ratio

Cache Hit Ratio = (Cache Hits / Total Requests) × 100

Example: 95% = excellent

---

## Improving Hit Ratio

Increase TTL
Use consistent query strings
Normalize headers
Prefetch content

---

## CDN Performance Optimization

TCP reuse
HTTP/2 & HTTP/3
Brotli compression

---

## Popular CDN Providers

Cloudflare
AWS CloudFront
Azure CDN
Akamai
Fastly
Google Cloud CDN

---

## What Content Should Use CDN?

### ✅ Great for CDN:

Static files
Videos
Downloads
Public APIs

### ❌ Not for CDN:

User-specific data
Dynamic content
Private content

---

## CDN Caching

### Cache-Control Headers

```id="p2xv1g"
Cache-Control: public, max-age=31536000, immutable
Cache-Control: public, max-age=3600
Cache-Control: no-cache, no-store, must-revalidate
Cache-Control: public, max-age=0, must-revalidate
```

---

## Cache Hierarchy

1. Browser Cache
2. CDN Edge Cache
3. CDN Regional Cache
4. Origin Server

---

## Real-World Examples

### Static Website

```html id="sx7fgx"
<img src="https://cdn.example.com/images/logo.png">
```

---

### Video Streaming

User → CDN → Smooth playback

---

### E-commerce Site

Images → CDN
Prices → Origin
CSS/JS → CDN

---

### Software Distribution

User downloads → CDN → Faster delivery

---

## CDN Configuration Examples

### Cloudflare Setup

1. Add domain
2. Update nameservers
3. Enable proxy
4. Configure cache rules

---

### AWS CloudFront

1. Create distribution
2. Set origin
3. Configure behaviors
4. Add domain
5. Add SSL

---

### Nginx as Simple CDN Cache

```nginx id="3j5dxq"
proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=cdn:100m max_size=10g;
```

---

## Cache Invalidation (Purging)

### Methods:

1. Cache Purging
2. Versioning
3. Cache-Control Headers

---

## CDN Performance Optimization

1. Enable Compression
2. Image Optimization
3. HTTP/2 & HTTP/3
4. Minification

---

## CDN Security Features

DDoS Protection
WAF
SSL/TLS
Access Control

---

## Monitoring CDN Performance

Cache Hit Ratio
Bandwidth Savings
Response Time

---

## Common Commands

```bash id="j7c1e2"
curl -I https://cdn.example.com/image.jpg
```

---

## Troubleshooting

Changes not reflected → cache issue
Slow first load → cache miss
Different regions → cache sync

---

## CDN Best Practices

Use long cache times
Version assets
Optimize images
Monitor hit ratio
Use separate domain

---

## Cost Considerations

Data transfer cost
Request cost
Free tiers available

---

## Key Takeaways

✅ CDNs serve content from geographically distributed servers
✅ Reduces latency by serving from nearest location
✅ Great for static content (images, CSS, JS, videos)
✅ Cache invalidation is important when content changes
✅ Versioned URLs are better than cache purging
✅ CDNs provide DDoS protection and improved security
✅ Monitor cache hit ratio (aim for >90%)
✅ Use separate domain for CDN content (cookieless)
✅ Most modern websites use CDNs for performance

---


