# Kubernetes Learning Notes 🚀

A comprehensive collection of Kubernetes concepts, best practices, and deployment strategies distilled from hands-on learning and courses. 

## Table of Contents
- [Core Concepts](#core-concepts)
- [Kubernetes Architecture](#kubernetes-architecture)
- [Key Components](#key-components)
- [Essential Commands](#essential-commands)
- [Deployment Strategies](#deployment-strategies)
- [Microservices Example](#microservices-example)
- [Local Development](#local-development)
- [Best Practices](#best-practices)
- [Learning Path](#learning-path)

---

## Core Concepts

### 🐳 **Containers & Docker**
- Package applications with all dependencies (app + system-level)
- Isolate applications from host OS and other containers
- **Docker** is the most popular containerization tool
- Dockerfiles define how to build container images

### ☸ **What is Kubernetes?**
- Container orchestration platform for deployment, scaling, and management
- Features:
  - Horizontal scaling with simple commands
  - Rolling updates with zero downtime
  - Self-healing capabilities
  - Declarative configuration model

---

## Kubernetes Architecture

### 🏗 **Cluster Components**
| Component       | Description |
|-----------------|-------------|
| **Control Plane** | Manages cluster (API Server, etcd, controllers, scheduler) |
| **Worker Nodes**  | Run applications (kubelet, kube-proxy, container runtime) |
| **Pods**         | Smallest deployable units (1+ containers sharing network/storage) |

### 🔗 **Networking**
- **Services** provide stable endpoints:
  - `ClusterIP`: Internal communication
  - `NodePort`: External access via node ports
  - `LoadBalancer`: Cloud provider integration

---

## Key Components

### 📦 **Pods**
- Ephemeral units containing 1+ containers
- Share network namespace and storage
- Best practice: Use multiple pods for scaling, not multiple containers in one pod

### 🔄 **ReplicaSets**
- Maintain desired number of pod replicas
- Self-healing: Automatically replaces failed pods
- Managed via label selectors

### 🚀 **Deployments**
- Higher-level abstraction over ReplicaSets
- Enable:
  - Rolling updates
  - Rollbacks
  - Pause/Resume functionality
- Preferred method for production workloads

---

## Essential Commands

### 🛠 **kubectl Cheat Sheet**
```bash
# Cluster info
kubectl get nodes
kubectl cluster-info

# Pod management
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>

# Deployment
kubectl apply -f deployment.yaml
kubectl scale deployment <name> --replicas=3

# Services
kubectl get services
kubectl expose deployment <name> --type=NodePort
```

### 📝 **YAML Structure**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image:latest
        ports:
        - containerPort: 80
```

---

## Deployment Strategies

### 🔄 **Rolling Updates**
- Gradual replacement of old pods with new ones
- Zero downtime during updates
- Automatic rollback if health checks fail

### ⚖ **Scaling**
- Manual scaling: `kubectl scale`
- Horizontal Pod Autoscaler (HPA) for automatic scaling (not covered in detail)

---

## Microservices Example

### 🗳 **Voting App Architecture**
```
Frontend (Python/Flask) → Redis → Worker (.NET) → PostgreSQL ← Results (Node.js)
```

- **Key Features**:
  - Multiple technologies in one application
  - Service discovery via DNS names
  - External access via NodePort (30004/30005)
  - Demonstrates inter-service communication

---

## Local Development

### 💻 **Minikube Setup**
1. Install hypervisor (VirtualBox recommended)
2. Install `kubectl`
3. Install Minikube
4. Start cluster:
   ```bash
   minikube start --driver=virtualbox
   ```
5. Verify:
   ```bash
   kubectl get nodes
   ```

---

## Best Practices

### ✅ **Do's**
- Use declarative YAML configurations
- Version control all Kubernetes manifests
- Prefer Deployments over manual Pod management
- Use Services for stable networking
- Implement proper resource requests/limits

### ❌ **Don'ts**
- Don't hardcode configurations
- Avoid manual Pod management in production
- Don't expose unnecessary services
- Avoid using `latest` tag in production

---

## Learning Path

### 📚 **Next Steps**
1. **Certifications**:
   - CKAD (Certified Kubernetes Application Developer)
   - CKA (Certified Kubernetes Administrator)
   
2. **Advanced Topics**:
   - Persistent storage
   - Secrets management
   - Network policies
   - Service meshes (Istio, Linkerd)

3. **Ecosystem Tools**:
   - Helm (package manager)
   - Argo CD (GitOps)
   - Prometheus (monitoring)

---

