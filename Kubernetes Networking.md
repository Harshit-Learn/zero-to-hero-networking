
---

# Kubernetes Networking  ( Day-12)

## What is Kubernetes Networking?

Kubernetes networking connects Pods, Services, and external clients in a cluster.

Kubernetes networking is fundamentally different from traditional networking. It's built on a set of requirements that enable seamless communication in a dynamic, container-orchestrated environment.

---

## The Kubernetes Network Model

Kubernetes imposes these fundamental requirements on any network implementation:

### 1. Every Pod gets its own IP address

Traditional: Containers share host IP, use port mapping
Kubernetes: Each Pod has unique IP in cluster

Pod A: 10.244.1.5
Pod B: 10.244.1.6
Pod C: 10.244.2.8 (on different node)

No port mapping needed
No NAT between Pods

---

### 2. Pods can communicate with all other Pods without NAT

Pod on Node A (10.244.1.5) can directly reach:

* Pod on Node A (10.244.1.6)
* Pod on Node B (10.244.2.8)

No address translation
No complex routing configuration

---

### 3. Agents on a node can communicate with all Pods

kubelet, kube-proxy (node agents) can reach any Pod

---

### 4. Pods in host network see same network as node

Normal Pod: Has own network namespace
Host network Pod: Shares node's network namespace

---

## Why This Model?

### Problem with Traditional Port Mapping:

Docker style:

Container A: localhost:8080 → Host port 30001
Container B: localhost:8080 → Host port 30002

Challenges:

* Port allocation management
* Service discovery complex
* No direct container-to-container
* Doesn't scale

---

### Kubernetes Model Benefits:

Pod A: 10.244.1.5:8080
Pod B: 10.244.1.6:8080

Benefits:

* Simple addressing (IP:Port)
* Direct communication
* Scales to thousands of Pods
* Service discovery easier

---

## How Kubernetes Achieves This

### CNI (Container Network Interface):

Kubernetes doesn't implement networking itself
Delegates to CNI plugins

When Pod starts:

1. Kubernetes calls CNI plugin
2. Plugin assigns IP, sets interface, routing
3. Pod ready

---

## Pods and IPs

### Pod Networking

Every Pod gets its own unique IP address.

```id="v3m8xk"
Kubernetes Cluster
    |
    ├── Node 1 (10.0.1.10)
    |    └── Pod Subnet: 10.244.1.0/24
    |         ├── Pod A: 10.244.1.5
    |         └── Pod B: 10.244.1.6
    |
    └── Node 2 (10.0.1.20)
         └── Pod Subnet: 10.244.2.0/24
              ├── Pod C: 10.244.2.8
              └── Pod D: 10.244.2.9
```

---

## Containers in a Pod

Containers in the same Pod share the same network namespace.

Pod: web-app (IP: 10.244.1.5)

* nginx → localhost:80
* logger → localhost:80

Shared:

* Same IP
* Same localhost
* Same ports

---

## Communication Patterns

Container-to-Container (same Pod)
Pod-to-Pod (different Pods)
External-to-Pod via Services

---

## Services

Services provide stable IP and DNS name for accessing Pods.

### Problem Services Solve

Pod IPs change when Pods restart

---

### Service Solution:

Service: web-app-service

* Stable IP: 10.96.0.10
* Stable DNS
* Load balancing

Clients connect to stable Service IP

---

## How Services Work

### ClusterIP

Virtual IP assigned to Service

### Endpoints

List of Pod IPs

### kube-proxy

Handles routing using:

* iptables
* IPVS

---

## Service Types

### 1. ClusterIP

Internal access only

---

### 2. NodePort

Exposes service on each node

```id="z2c3xl"
Node1:30080
Node2:30080
Node3:30080
```

---

### 3. LoadBalancer

External cloud load balancer

---

### 4. ExternalName

Maps service to DNS

---

## Service Discovery (DNS)

Service name → DNS

backend.default.svc.cluster.local

---

## Ingress

Ingress exposes HTTP/HTTPS routes to services.

```id="m4q9tx"
Ingress → Services → Pods
```

Routes based on:

* Host
* Path

---

## Popular Ingress Controllers

Nginx
Traefik
HAProxy
AWS ALB
Istio

---

## Real-World Examples

### Simple Web Application

Frontend → backend service

---

### Microservices with Ingress

```id="n9x2pt"
api.example.com/users → user-service
api.example.com/orders → order-service
```

---

## Network Policies

Control traffic between Pods

Default: Allow all

With policy: Restrict access

---

## CNI (Container Network Interface)

CNI plugins provide networking

---

## Popular CNI Plugins

Calico
Flannel
Cilium
Weave
Canal

---

## CNI Plugin Comparison

| Plugin  | Type    | Performance | Policies  | Use Case         |
| ------- | ------- | ----------- | --------- | ---------------- |
| Calico  | L3      | High        | Excellent | Production       |
| Flannel | Overlay | Medium      | Limited   | Simple           |
| Cilium  | eBPF    | Very High   | Excellent | High-performance |
| Weave   | Mesh    | Medium      | Good      | Multi-cloud      |
| Canal   | Hybrid  | Medium      | Excellent | Balanced         |

---

## Cross-Node Traffic

Pod → Node → Other Node → Pod

Handled by CNI

---

## Common Networking Commands

```bash id="k3p2vo"
kubectl get svc
kubectl get pods -o wide
kubectl describe svc my-service
kubectl exec -it my-pod -- curl http://service
kubectl port-forward svc/my-service 8080:80
```

---

## Troubleshooting

Service not reachable → check endpoints
External access → check type
Ingress issues → check controller

---

## Best Practices

Use Services instead of Pod IPs
Use DNS names
Implement Network Policies
Use Ingress for HTTP
Use health checks

---

## Key Takeaways

* Each Pod gets a unique IP address
* Services provide stable DNS names and IPs
* ClusterIP for internal, LoadBalancer for external
* Ingress routes HTTP(S) traffic to Services
* DNS resolution: service-name.namespace.svc.cluster.local
* Network Policies control Pod-to-Pod traffic
* CNI plugins handle actual networking
* Use Service names, not Pod IPs
* Port-forward for debugging: kubectl port-forward
* Always implement Network Policies in production

---


