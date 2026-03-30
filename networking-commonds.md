
---

# 📖 Table of Contents

* Basic Connectivity
* IP & Network Info
* DNS Commands
* Port & Connection Commands
* Internet & API Testing
* Troubleshooting Commands
* Real-Life Debugging Scenarios
* Interview Tips

---

# 🔹 1. Basic Connectivity Commands

## ✅ `ping`

Check if a server is reachable.

```bash
ping google.com
```

📌 **Use Case:**

* Check internet working or not
* Verify server is alive

📊 **Real Life:**

* If `Request timed out` → server/network issue
* If reply comes → connection OK

---

## ✅ `tracert` (Windows) / `traceroute` (Linux)

Track path of packets.

```bash
tracert google.com
```

📌 **Use Case:**

* Identify where network is slow or blocked

📊 **Real Life:**

* If stuck at a hop → ISP or firewall issue

---

# 🔹 2. IP & Network Info

## ✅ `ipconfig` (Windows)

```bash
ipconfig
```

📌 **Important Fields:**

* IPv4 Address → Your system IP
* Default Gateway → Router IP

📊 **Real Life:**

* No IP → DHCP issue
* Wrong gateway → No internet

---

## ✅ `ip a` (Linux)

```bash
ip a
```

📌 Modern replacement of `ifconfig`

---

## ✅ `hostname`

```bash
hostname
```

📌 Shows system name (used in servers & logs)

---

# 🔹 3. DNS Commands

## ✅ `nslookup`

```bash
nslookup google.com
```

📌 **Use Case:**

* Convert domain → IP
* Check DNS working

📊 **Real Life:**

* If fails → DNS issue

---

## ✅ `dig` (Linux)

```bash
dig google.com
```

📌 Advanced DNS debugging tool

---

# 🔹 4. Port & Connection Commands

## ✅ `netstat`

```bash
netstat -ano
```

📌 **Use Case:**

* Check open ports
* Identify process using port

📊 **Real Life:**

* Port already in use → app won’t start

---

## ✅ `ss` (Linux)

```bash
ss -tuln
```

📌 Faster version of netstat

---

## ✅ `telnet`

```bash
telnet google.com 80
```

📌 **Use Case:**

* Check if port is open

📊 **Real Life:**

* Connection refused → port blocked

---

## ✅ `nc` (Netcat)

```bash
nc -zv google.com 443
```

📌 Advanced port testing

---

# 🔹 5. Internet & API Testing

## ✅ `curl`

```bash
curl https://api.github.com
```

📌 **Use Case:**

* API testing
* Backend debugging

📊 **Real Life:**

* Used in QA & DevOps daily

---

## ✅ `wget`

```bash
wget https://example.com/file.zip
```

📌 Download files from internet

---

# 🔹 6. Troubleshooting Commands

## ✅ Flush DNS

```bash
ipconfig /flushdns   # Windows
```

📌 Fix DNS cache issues

---

## ✅ Restart Network (Linux)

```bash
sudo systemctl restart NetworkManager
```

---

## ✅ Check Internet via IP

```bash
ping 8.8.8.8
```

📊 **Logic:**

* Works → Internet OK
* Not working → Network issue

---

# 🧠 7. Real-Life Debugging Flow (IMPORTANT 🚀)

👉 When internet not working:

```bash
1. ping 127.0.0.1
```

✔ Check local system

```bash
2. ipconfig / ip a
```

✔ Check IP assigned

```bash
3. ping 8.8.8.8
```

✔ Check internet

```bash
4. nslookup google.com
```

✔ Check DNS

```bash
5. tracert google.com
```

✔ Find where issue occurs

---

# 💼 8. Real-Life Scenarios

## 🔥 Scenario 1: Website Not Opening

* `ping google.com` ❌
* `ping 8.8.8.8` ✅

👉 Problem = DNS

---

## 🔥 Scenario 2: Application Not Starting

* `netstat -ano`
  👉 Port already in use

---

## 🔥 Scenario 3: API Not Working

* `curl API_URL`

👉 Debug response

---

## 🔥 Scenario 4: Server Not Reachable

* `tracert server_ip`

👉 Find network break point

---

# 🎯 9. Most Important Commands (Focus First)

```bash
ping
ipconfig / ip a
nslookup
netstat
curl
tracert
telnet
```

---



# ⭐ Pro Tips

* Always debug step-by-step (don’t guess)
* Learn difference between:

  * Network issue 🌐
  * DNS issue 🌍
  * Application issue ⚙️

---

# 📌 Conclusion

Networking commands are **daily tools** for debugging real-world issues.
Mastering them = **strong foundation for DevOps & Cloud 🚀**

---

