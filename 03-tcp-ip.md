
---

# 🌐 TCP/IP & OSI Model (Day 3)

## 📌 What is TCP/IP?

TCP/IP (Transmission Control Protocol/Internet Protocol) is the fundamental communication protocol suite that powers the internet and most modern networks. It's not a single protocol but a collection of protocols working together at different layers.

---

## ❓ Why TCP/IP Exists

### The Problem:

Different computer systems and networks couldn't communicate because they used incompatible protocols.

### The Solution:

TCP/IP provides a standardized set of rules that all devices follow, enabling:

* Reliable data transmission across unreliable networks
* Interoperability between different systems and vendors
* End-to-end connectivity across multiple networks
* Error detection and recovery

---

## 🧩 TCP/IP Protocol Suite

TCP/IP is actually a family of protocols:

* **Application Layer:** HTTP, FTP, SMTP, DNS, SSH
* **Transport Layer:** TCP, UDP
* **Internet Layer:** IP, ICMP, ARP
* **Link Layer:** Ethernet, WiFi

---

## 🔑 The Two Main Protocols

---

## 1️⃣ TCP (Transmission Control Protocol)

TCP is a connection-oriented protocol that provides reliable, ordered delivery of data.

### 🔄 How TCP Ensures Reliability

#### ✔ Acknowledgments

Every packet received is acknowledged

```
Sender: Sends packet #1  
Receiver: Receives packet #1, sends ACK #1  
Sender: Receives ACK #1, now sends packet #2  
```

#### ✔ Sequence Numbers

Packets are numbered so they can be reassembled in order

```
Packet 1 (Seq: 1-100)  
Packet 2 (Seq: 101-200)  
Packet 3 (Seq: 201-300)  
```

If packets arrive out of order → receiver reorders them.

#### ✔ Retransmission

If ACK not received → packet is resent

```
Sender: Sends packet #1  
[Packet lost]  
Sender: Timeout → Resends packet #1  
Receiver: Sends ACK  
```

#### ✔ Flow Control

Prevents sender from overwhelming receiver

* Receiver shares window size
* Sender adjusts speed

#### ✔ Congestion Control

* Slow Start
* Congestion Avoidance
* Fast Retransmit

---

### 📌 TCP Characteristics

* Reliable
* Ordered
* Connection-based
* Error checking
* Higher overhead

👉 Use cases:

* HTTP
* SMTP
* FTP
* SSH

👉 Real-world analogy: Like a phone call 📞

---

## 2️⃣ UDP (User Datagram Protocol)

UDP is a connectionless protocol that provides fast but unreliable delivery.

### ⚡ How UDP Works

#### ✔ Fire and Forget

* No connection setup
* No ACK

#### ✔ No Ordering

Packets may arrive out of order

#### ✔ No Retransmission

Lost packets are not resent

---

### 📌 UDP Characteristics

* Fast
* Low latency
* Unreliable
* No ordering
* Lightweight

👉 Use cases:

* Video streaming
* Online gaming
* DNS
* VoIP

👉 Real-world analogy: Like postcards 📮

---

## 🤝 TCP Three-Way Handshake

Before data transfer, TCP establishes a connection.

```
Client                Server

SYN  ------------->  
       <-----------  SYN-ACK  
ACK  ------------->  
```

### 🔍 Steps

1. SYN → Client requests connection
2. SYN-ACK → Server responds
3. ACK → Connection established

---

## ❌ Connection Termination (Four-Way Handshake)

```
Client                Server

FIN  ------------->  
       <-----------  ACK  
       <-----------  FIN  
ACK  ------------->  
```

---

## 🔢 Ports

Ports are 16-bit numbers (0–65535) that help direct traffic to the right application.

### 📌 Example

* Port 80 → Web Server
* Port 22 → SSH
* Port 3306 → MySQL

---

## 🔗 Socket

```
Socket = IP Address : Port
```

👉 Example:

* 192.168.1.10:80
* 192.168.1.10:22

---

## 🧠 Port States

* LISTENING
* ESTABLISHED
* TIME_WAIT
* CLOSE_WAIT

---

## 🔄 Ephemeral Ports

Temporary ports used by client

* Linux: 32768–60999
* Windows: 49152–65535

---

## 📊 Common Ports

| Port  | Service          | Protocol |
| ----- | ---------------- | -------- |
| 22    | SSH              | TCP      |
| 80    | HTTP             | TCP      |
| 443   | HTTPS            | TCP      |
| 53    | DNS              | UDP/TCP  |
| 3306  | MySQL            | TCP      |
| 5432  | PostgreSQL       | TCP      |
| 6379  | Redis            | TCP      |
| 27017 | MongoDB          | TCP      |
| 3000  | Dev servers      | TCP      |
| 8080  | Alternative HTTP | TCP      |

---

## 📊 Port Ranges

* 0–1023 → Well-known
* 1024–49151 → Registered
* 49152–65535 → Dynamic

---

## 🧠 OSI Model (7 Layers)

| Layer | Name         | Function        | Example  |
| ----- | ------------ | --------------- | -------- |
| 7     | Application  | Apps/services   | HTTP     |
| 6     | Presentation | Formatting      | SSL/TLS  |
| 5     | Session      | Connection mgmt | RPC      |
| 4     | Transport    | Delivery        | TCP/UDP  |
| 3     | Network      | Routing         | IP       |
| 2     | Data Link    | Node transfer   | Ethernet |
| 1     | Physical     | Signals         | Cable    |

👉 Mnemonic: *Please Do Not Throw Sausage Pizza Away* 🍕

---

## 🌐 TCP/IP Model (4 Layers)

| Layer          | OSI Mapping | Protocols |
| -------------- | ----------- | --------- |
| Application    | 5,6,7       | HTTP, DNS |
| Transport      | 4           | TCP, UDP  |
| Internet       | 3           | IP        |
| Network Access | 1,2         | Ethernet  |

---

## 🛠️ Real-World DevOps Examples

### 🔹 Web App Flow

```
Browser → Load Balancer → Web Server → Database
```

---

### 🔹 Kubernetes Flow

```
Frontend → Backend → Redis
```

---

### 🔹 Debugging Commands

```bash
telnet example.com 80
nc -zv example.com 80
lsof -i :8080
netstat -ano | findstr :8080
```

---

## 🔄 Network Traffic Flow

When visiting a website:

* Application → HTTP
* Transport → TCP
* Network → IP
* Data Link → MAC
* Physical → Signals

---

## ⚙️ Key Concepts for DevOps

### 🔹 Connection States

* ESTABLISHED
* LISTENING
* TIME_WAIT

```bash
netstat -an
ss -tuln
```

---

### 🔹 Firewalls & Ports

* AWS Security Groups
* Azure NSG
* GCP Firewall
* iptables

---

### 🔹 Health Checks

Load balancer checks backend using TCP

---

## ✅ Key Takeaways

* TCP = Reliable but slower
* UDP = Fast but unreliable
* Ports = Identify services
* Handshake = Connection setup
* Layers = Help debugging
* DevOps works mostly on Layer 4 & 7

---



