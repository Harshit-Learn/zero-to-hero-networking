

---

# 🌐 Networking Fundamentals (Day 1)

## 📌 What is Networking?

Networking means connecting multiple devices so they can communicate and share data with each other.

👉 Example:

* Mobile connected to WiFi
* Laptop accessing the Internet
* Office computers connected together

---

## 🌍 What is Internet?

The Internet is a **global network of networks**.

👉 In simple terms:

* Computers around the world are connected
* They communicate using defined rules (protocols)

👉 Real-life example:

* When you open Google → your request goes to a server → the response comes back to your device

---

## 🖥️ Client–Server Model

In networking, communication happens between:

* Client → Requests data (browser, mobile app)
* Server → Provides data (web server)

👉 Example:
Client (your browser) → sends request → Server → sends response

---

## 🌐 What is ISP?

ISP (Internet Service Provider) is a company that provides internet access.

👉 Examples:

* Airtel
* Jio
* BSNL

Your modem/router connects to ISP to access the internet.

---

## 🧩 Types of Networks

### 1️⃣ LAN (Local Area Network)

* Small network (home, office)
* High speed

👉 Example: Home WiFi

---

### 2️⃣ WAN (Wide Area Network)

* Large network (cities, countries)
* Internet is the biggest WAN

---

### 3️⃣ MAN (Metropolitan Area Network)

* Covers a city or large campus

---

## 📶 Wired vs Wireless Network

### Wired Network

* Uses cables (Ethernet)
* Faster and more stable

### Wireless Network

* Uses WiFi
* Flexible but slightly less stable

---

## 🔌 Network Devices

### 🖥️ 1. Modem

* Converts internet signal into digital form
* Connects your network to ISP

👉 Simple: Entry point of Internet

---

### 📡 2. Router

* Connects multiple devices
* Sends data to the correct destination

👉 Example: WiFi router

---

### 🔀 3. Switch

* Connects devices within a LAN
* Sends data to the specific device

---

### 🔁 4. Hub (Old Device)

* Sends data to all devices
* Not intelligent

---

## 🧠 What is MAC Address?

A MAC Address is a **unique hardware address** assigned to every network device.

👉 Features:

* Physical address
* Permanent
* Assigned by manufacturer

👉 Example:

```bash
00:1A:2B:3C:4D:5E
```

---

## 📦 What is a Packet?

Data is sent over the network in small units called packets.

Each packet contains:

* Source
* Destination
* Data

Packets travel independently and are reassembled at the destination.

---

## 🔄 How Data Moves (Basic Flow)

1. You send a request from your browser
2. Device → Router → Internet
3. Server processes the request
4. Response comes back to your device

👉 This is the basic foundation of networking

---

## 🔄 Upload vs Download

* Upload → Sending data (your device → internet)
* Download → Receiving data (internet → your device)

---

## 🔁 Duplex Communication

### Half Duplex

* One direction at a time

### Full Duplex

* Both directions at the same time

👉 Example:

* Phone call = Full duplex
* Walkie-talkie = Half duplex

---

## ⚡ Important Concepts


# 📘 Networking & System Design Basics (DevOps)

---

## 🔹 1. Latency (Most Important)

👉 **Meaning:** Time taken for data to travel from one point to another

📌 **Example:**
Delhi → Mumbai server request
If it takes **50 ms → Latency = 50ms**

👉 **Simple Understanding:**
Like delay in a phone call 📞

✅ **Low latency = Fast system**

---

## 🔹 2. Bandwidth

👉 **Meaning:** Amount of data that can be transferred at a time

📌 **Example:**
100 Mbps vs 10 Mbps internet

👉 **Simple Understanding:**
Pipe jitna mota → utna zyada pani (data)

✅ **Higher bandwidth = More data transfer**

---

## 🔹 3. Throughput

👉 **Meaning:** Actual data successfully transferred

📌 **Key Point:**

* Bandwidth = Theoretical
* Throughput = Real performance

👉 **Simple Understanding:**
6-lane road (bandwidth)
Traffic ki wajah se sirf 3 lane chal rahi (throughput)

---

## 🔹 4. Availability

👉 **Meaning:** System kitna time available hai (uptime)

📌 **Example:**
99.9% uptime

👉 **Simple:**
Server hamesha accessible hona chahiye

---

## 🔹 5. Scalability

👉 **Meaning:** Load badhne par system expand ho sakta hai

📌 **Example:**
Website traffic badhne par auto scaling

### 🔸 Types:

* **Vertical Scaling:** Machine powerful banana
* **Horizontal Scaling:** Machines increase karna

---

## 🔹 6. Elasticity

👉 **Meaning:** Demand ke hisaab se resources auto increase/decrease

👉 **Simple:**

* Load zyada → resources add
* Load kam → resources remove

---

## 🔹 7. Fault Tolerance

👉 **Meaning:** Failure ke baad bhi system chalta rahe

📌 **Example:**
1 server down → dusra automatically handle kare

---

## 🔹 8. High Availability (HA)

👉 **Meaning:** System always accessible rahe, downtime minimum ho

📌 **Achieved By:**

* Multiple servers
* Load balancing

---

## 🔹 9. Load Balancing

👉 **Meaning:** Traffic ko multiple servers me distribute karna

👉 **Simple:**
1 counter ki bheed → 5 counters me divide

---

## 🔹 10. CDN (Content Delivery Network)

👉 **Meaning:** Data nearest server se serve hota hai

📌 **Example:**

* Delhi user → Delhi server
* USA user → USA server

✅ **Benefit:** Lower latency

---

## 🔹 11. Region & Availability Zone (AWS Concept)

👉 From [Amazon Web Services (AWS)](https://aws.amazon.com?utm_source=chatgpt.com)

* **Region:** Geographic area (e.g., Mumbai)
* **Availability Zone (AZ):** Multiple data centers within a region

✅ **Use:**

* High availability
* Fault tolerance

---

## 🔹 12. IOPS (Input/Output Operations Per Second)

👉 **Meaning:** Disk read/write speed

✅ **High IOPS = Faster database performance**

---

## 🔹 13. Auto Scaling

👉 **Meaning:** Automatically servers add/remove based on traffic

---

## 🔹 14. Virtualization

👉 **Meaning:** One physical machine → multiple virtual machines

✅ **Base of cloud computing**

---


👉 **Question:** Difference between Latency & Bandwidth

✅ **Answer:**

* **Latency = Delay (Time)**
* **Bandwidth = Capacity (Data size)**

---



## 🛠️ Real Life Example

👉 When you play a YouTube video:

* Request → Internet → Server
* Server → sends video data → your device
* Router ensures correct delivery

---

## ✅ Key Takeaways

* Networking = connection of devices
* Internet = network of networks
* Client–Server = communication model
* Router = decides path
* Switch = sends data within LAN
* MAC Address = unique device ID
* Packet = unit of data
✔ Protocol = communication rules

---

