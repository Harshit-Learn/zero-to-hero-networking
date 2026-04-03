
---

# 🔐 VPN & Tunneling ( Day-8)

## What is a VPN?

VPN (Virtual Private Network) creates a secure, encrypted connection over a public network (like the internet).

---

# The Core Problem VPNs Solve

Scenario: Company has office in New York and branch in London.

---

## Option 1: Dedicated Line (Pre-VPN Solution)

New York Office ←------- Leased Line -------→ London Office
(Very expensive physical cable)

Cost: $10,000+/month
Advantages: Secure, private, high bandwidth
Disadvantages: Extremely expensive, inflexible, long setup time

---

## Option 2: VPN (Modern Solution)

New York Office ←------ Internet ------→ London Office
(Encrypted tunnel through public internet)

Cost: $50/month + internet
Advantages: Cheap, flexible, quick setup
Disadvantages: Dependent on internet quality

VPN creates "virtual" private network over public infrastructure. 

---

# What VPN Actually Does

## 1. Encapsulation (Tunneling)

Original Packet:
[IP Header][TCP Header][Data: "secret message"]

After VPN Encapsulation:
[VPN IP Header][VPN Header][Encrypted:[IP Header][TCP Header][Data: "secret message"]]
↑                            ↑
Outer packet             Inner packet (encrypted)
(for internet routing)   (actual data, hidden)

---

## 2. Encryption

Without VPN:
Your Computer → "username=admin&password=secret" → Website
(ISP, government, hackers can read this)

With VPN:
Your Computer → VPN: "a7f3b9c2d..." → Website
(ISP sees encrypted gibberish)

VPN Server → "username=admin&password=secret" → Website
(Decrypted at VPN server)

---

## 3. IP Address Masking

Your Real IP: 203.0.113.5 (New York)
↓
VPN Tunnel
↓
VPN Server IP: 198.51.100.10 (London)
↓
Website

Website sees: 198.51.100.10 (thinks you're in London)

---

# VPN Components

## VPN Client

Software on your device

Initiates VPN connection
Encrypts outbound traffic
Decrypts inbound traffic
Routes traffic through tunnel

---

## VPN Server

Endpoint on remote network

Accepts VPN connections
Decrypts traffic from clients
Encrypts traffic to clients
Routes traffic to destination

---

## VPN Protocol

Rules for establishing and maintaining connection

Authentication method
Encryption algorithm
Key exchange mechanism
Encapsulation format

---

## VPN Tunnel

Virtual encrypted connection

Logical path through public network
All traffic encrypted within tunnel
Appears as single connection to outside observer

---

# Types of VPNs

## 1. Remote Access VPN

Connects individual users to a private network.

Remote Worker (Home)
|
[VPN Client]
|
Internet
|
[VPN Server]
|
Company Network

Use case: Working from home, accessing company resources.

---

## 2. Site-to-Site VPN

Connects entire networks together.

Office A Network
|
[VPN Gateway]
|
Internet
|
[VPN Gateway]
|
Office B Network

Use case: Connecting branch offices, connecting on-premise to cloud.

---

## 3. Cloud VPN

Connects your network to cloud resources.

On-Premise Network
|
[VPN Gateway]
|
Internet
|
[Cloud VPN Gateway]
|
AWS/Azure/GCP VPC

Use case: Hybrid cloud architecture.

---

# How VPN Works

1. Your Computer
   ↓ (Data is encrypted)
2. VPN Client
   ↓ (Encrypted tunnel through internet)
3. VPN Server
   ↓ (Data is decrypted)
4. Destination (Website/Server)

Without VPN:

Your IP: 203.0.113.5 → Website sees: 203.0.113.5

With VPN:

Your IP: 203.0.113.5 → VPN → Website sees: 198.51.100.10 (VPN server IP)

---

# VPN Protocols

VPN protocols define how the VPN tunnel is created and maintained. Each has different characteristics.

---

## OpenVPN

### Architecture:

Open-source (auditable code)
Uses OpenSSL library for encryption
Custom protocol built on SSL/TLS
Highly configurable

### How it works:

1. Client initiates connection to OpenVPN server
2. TLS handshake (like HTTPS):

   * Certificate verification
   * Key exchange
   * Encryption negotiation
3. Virtual network interface created (tun/tap)
4. Traffic routed through encrypted tunnel

### Encryption:

Supports multiple algorithms: AES-256, ChaCha20, Blowfish
Perfect Forward Secrecy (PFS): New keys per session
HMAC authentication: SHA-256, SHA-512

### Transport:

TCP Mode: Reliable, slower, works everywhere
UDP Mode: Faster, preferred for VPN

### Why TCP vs UDP matters:

UDP Mode (Recommended):

* Lower latency
* Better for VoIP, gaming, streaming
* Handles packet loss at application layer

TCP Mode:

* Works through restrictive firewalls
* Reliable, but slower
* TCP-over-TCP problem (reliability overkill)

### Advantages:

Most secure (proven track record)
Works on all platforms
Bypasses most firewalls
Flexible configuration

### Disadvantages:

Slower than WireGuard
Complex configuration
Requires third-party client software

---

## WireGuard

### Architecture:

Modern, minimalist design
~4,000 lines of code (vs OpenVPN's 400,000)
Built into Linux kernel
Uses state-of-the-art cryptography

### Cryptography (No Options - Simplicity):

Encryption: ChaCha20
Authentication: Poly1305
Key Exchange: Curve25519
Hash: BLAKE2s

### Why Fixed Cryptography?:

OpenVPN: User chooses algorithm (can choose weak ones)
WireGuard: Only modern, secure algorithms available
Result: Simpler, impossible to misconfigure

### How it works:

1. Pre-shared public keys (like SSH keys)
2. No handshake needed (stateless)
3. Cryptokey routing: IP addresses mapped to public keys
4. Extremely fast connection setup

### Key Features:

Roaming:

You're on WiFi (IP: 192.168.1.100)
↓
Switch to 4G (IP: 10.0.0.50)
↓
WireGuard automatically maintains connection

Performance:

OpenVPN: 100 Mbps
IPSec: 400 Mbps
WireGuard: 1000 Mbps

WireGuard is 10x faster than OpenVPN

### Advantages:

Extremely fast
Simple configuration
Built into Linux kernel (5.6+)
Mobile-friendly
Strong security

### Disadvantages:

Newer
Static IP assignment
Requires modern systems

---

## IPSec (Internet Protocol Security)

Architecture:

Industry standard
Built into many operating systems
Suite of protocols
Complex but powerful

---

## SSL/TLS VPN

Uses HTTPS (port 443)
Works in browser

---

# Protocol Comparison

| Feature          | OpenVPN   | WireGuard | IPSec     | SSL VPN |
| ---------------- | --------- | --------- | --------- | ------- |
| Speed            | Medium    | Fastest   | Fast      | Slowest |
| Security         | Excellent | Excellent | Excellent | Good    |
| Ease of Setup    | Medium    | Easy      | Difficult | Easy    |
| Platform Support | All       | Most      | All       | All     |

---

# Tunneling Concepts

Tunneling is the process of encapsulating one network protocol inside another.

---

# Key Takeaways

* VPNs create encrypted tunnels over public networks
* Remote access VPN for individuals, site-to-site for networks
* WireGuard is modern and fast, OpenVPN is mature and flexible
* SSH tunneling is simple for quick port forwarding
* Cloud VPNs connect on-premise to cloud (hybrid cloud)
* Split tunneling sends only some traffic through VPN
* Always use VPN on public WiFi for security
* Check firewall and routing when troubleshooting VPN issues

---


