

# Docker Networking ( Day-11)

## What is Docker Networking?

Docker networking allows containers to communicate with each other and with the outside world.

---

## The Container Networking Problem

### Traditional VMs:

Each VM has:

* Virtual network adapter
* Own IP address
* Acts like physical machine
* Full network stack

Simple, but heavy

---

### Containers:

Containers share host kernel
Multiple containers on one host
Need network isolation between containers
But also need to communicate

Challenge: Provide isolation + connectivity efficiently

---

## Docker's Solution:

Network Namespaces: Isolate network stack per container
Virtual Ethernet Pairs: Connect containers to networks
Bridge Networks: Software switches connecting containers
Port Mapping: NAT to expose containers to host

---

## Linux Network Namespaces

### What is a Network Namespace?

A namespace is an isolated network stack:

Each namespace has its own:

* Network interfaces
* IP addresses
* Routing table
* Firewall rules
* Port space

Containers share kernel but have separate network namespaces

---

### How It Works:

Host Network Namespace:

* eth0: 192.168.1.100
* Ports: SSH on 22, etc.

Container 1 Namespace:

* eth0: 172.17.0.2
* Ports: App on 80

Container 2 Namespace:

* eth0: 172.17.0.3
* Ports: App on 80

Complete isolation: Each has its own "localhost"

---

## Virtual Ethernet Pairs (veth)

### The Connection Mechanism:

veth pair = Two virtual network interfaces connected like a cable

One end in host namespace
Other end in container namespace

```id="r1h1bo"
        Host Namespace          |    Container Namespace
                               |
    vethXXXX (host side) ←---cable---→ eth0 (container side)
         ↓                     |           ↓
    Docker Bridge             |       App in container
```

---

## Data Flow:

1. Container sends packet to eth0
2. Packet travels through veth pair
3. Emerges at host
4. Host processes/routes packet

---

## Docker Network Drivers

Docker provides different network drivers for different use cases.

---

## 1. Bridge (Default)

### What It Is:

Software network switch (Linux bridge)

---

### How It Works:

```id="v6dpt3"
        Host
         |
    docker0 bridge (172.17.0.1)
         |
    ┌────┴────┬────────┐
    |         |        |
  veth1     veth2    veth3
    |         |        |
Container1 Container2 Container3
172.17.0.2 172.17.0.3 172.17.0.4
```

---

### Packet Flow (Container to Container):

1. Container1 sends to Container2
2. → eth0
3. → veth
4. → docker0
5. → veth
6. → eth0
7. Received

---

### Packet Flow (Container to Internet):

1. Container sends request
2. docker0 bridge
3. Host NAT
4. Internet
5. Response back

---

## Default Bridge Limitations:

* No automatic DNS resolution
* All containers same network
* Legacy features

---

## User-Defined Bridge:

```bash id="y3x5po"
docker network create my-network
```

Benefits:

* DNS resolution
* Isolation
* Dynamic containers

---

## 2. Host

### What It Is:

Container shares host network

```bash id="1c2p7s"
docker run --network host nginx
```

---

Implications:

* Uses host ports
* No port mapping
* Possible conflicts

---

## 3. None

### What It Is:

No networking

```bash id="zqxtm7"
docker run --network none my-app
```

Only loopback available

---

## 4. Overlay

### What It Is:

Multi-host network using VXLAN

```id="y5kptq"
Container1 → Overlay → Container2
```

Works across multiple hosts

---

## 5. Macvlan

### What It Is:

Container gets real IP

```bash id="j1ldh0"
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=eth0 macvlan-net
```

---

## Default Docker Networks

```bash id="9qkq8m"
docker network ls
```

---

## Creating Custom Networks

```bash id="7f3fpr"
docker network create my-network
```

---

## Container Communication

### By Container Name (DNS)

```bash id="v9x0r9"
ping postgres-db
```

---

### By IP Address

```bash id="1q7dox"
docker inspect postgres-db | grep IPAddress
```

---

## Port Mapping

```bash id="y8x1bc"
docker run -p 8080:80 nginx
```

Host:8080 → Container:80

---

## Real-World Examples

### Web App with Database

```bash id="d5l2tv"
docker network create myapp-network
```

---

### Microservices

```bash id="4s0hxl"
docker network create microservices
```

---

### Docker Compose

```yaml id="1o0r3d"
version: '3.8'
services:
  web:
    image: nginx
```

---

## Container DNS Resolution

Docker DNS: 127.0.0.11

```bash id="fw3p3o"
ping api
```

---

## Network Isolation

Containers on different networks can't communicate

---

## Common Networking Commands

```bash id="v6tx8k"
docker network ls
docker network create my-network
docker network inspect my-network
docker network rm my-network
docker network prune
```

---

## Troubleshooting

### Containers Can't Communicate

```bash id="o2goxx"
docker exec container1 ping container2
```

---

### Port Already in Use

```bash id="cv7zz2"
lsof -i :8080
```

---

### Can't Access Container

```bash id="8a9z3m"
curl http://localhost:8080
```

---

## Docker Network Security

Isolate services
Use internal networks
Custom subnets

---

## Docker Network Performance

Use host network for performance
Use overlay for multi-host

---

## Common Patterns

Frontend-Backend separation
Service mesh
Zero-trust

---

## Key Takeaways

✅ Docker creates isolated networks for containers
✅ Bridge is the default network driver
✅ Containers on same network can communicate by name
✅ Use custom networks instead of default bridge
✅ Port mapping: -p host:container
✅ Docker Compose automatically creates networks
✅ DNS resolution works for container names
✅ Network isolation improves security
✅ Use docker network commands to manage networks
✅ Always use user-defined networks for production

---


