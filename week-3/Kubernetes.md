# Kubernetes (K8s) Notes

## What is Kubernetes?

Kubernetes (K8s) is a powerful container orchestration tool that helps manage and scale containerized applications automatically.

**Think of Kubernetes like a traffic controller for your applications**, ensuring everything runs smoothly, even when demand increases or servers fail.

---

### 🛠 Real-Life Example

Imagine you run a food delivery service like Swiggy or Zomato. Your application needs to handle thousands of orders at once.

- **Without Kubernetes:** You manually add/remove servers to manage traffic — slow and inefficient.
- **With Kubernetes:** It automatically scales services based on demand, restarts failed services, and balances traffic.

---

## 🎯 Main Purpose of Kubernetes

Kubernetes helps in:

✅ Scaling applications automatically (e.g., more users during peak hours)  
✅ Ensuring high availability (e.g., restarting services when they fail)  
✅ Load balancing (e.g., distributing orders evenly)  
✅ Efficient resource utilization (e.g., avoiding wasted servers)  
✅ Automating deployments & updates (e.g., app updates without downtime)

---

## 🧠 Kubernetes Architecture Overview

Kubernetes has two main layers:

1. **Control Plane** (Management Layer)  
2. **Worker Nodes** (Execution Layer)

---

### 1️⃣ Control Plane – Brain of Kubernetes

**Key Components:**

- **API Server:** Entry point for all commands (like a restaurant’s front desk)
- **Scheduler:** Assigns pods to nodes (like a dispatcher)
- **Controller Manager:** Maintains desired state (like a supervisor)
- **etcd:** Key-value database for storing cluster state (like order history)

---

### 2️⃣ Worker Nodes – Chefs & Kitchens

**Key Components:**

- **Kubelet:** Ensures containers are running (like a kitchen manager)
- **Container Runtime (Docker, containerd):** Runs containers (like chefs)
- **Kube-Proxy:** Manages internal traffic (like waiters)

---

## ⚙️ Kubernetes Key Resources

| Resource      | Purpose                                             | Analogy                                        |
|---------------|-----------------------------------------------------|------------------------------------------------|
| Pod           | Smallest deployable unit (1+ containers)            | A single food order                            |
| Deployment    | Manages replica sets & rolling updates              | A team of chefs                                |
| Service       | Exposes pods via stable endpoint                    | Restaurant front desk                          |
| Ingress       | Manages external HTTP traffic                       | Food delivery app                              |
| ConfigMap     | Stores non-sensitive configuration data             | Public recipe book                             |
| Secret        | Stores sensitive info like passwords                | Secret sauce recipe                            |

---

## 🧩 Kubernetes Key Components (Explained with Real-Life Examples)

### 🔹 kubectl (Command-Line Tool)

**What:** Interacts with the Kubernetes cluster.  
**Example:** Like placing an order through a delivery app.

#### Common Commands:
```bash
kubectl get nodes                        # View cluster nodes
kubectl get pods                         # List running pods
kubectl describe pod <pod-name>         # Pod details
kubectl delete pod <pod-name>           # Delete a pod
kubectl scale deployment myapp --replicas=5  # Scale to 5 replicas
```

---

### 🔹 Kubelet (Worker Node Agent)

**What:** Ensures containers are running as expected.  
**Example:** Like a kitchen manager making sure meals are being prepared.

---

### 🔹 API Server (Main Communication Hub)

**What:** Processes requests and communicates with other components.  
**Example:** Like a restaurant's front desk receiving and routing orders.

---

### 🔹 etcd (Configuration Database)

**What:** Stores cluster config and state.  
**Example:** Order history database.

---

### 🔹 Scheduler

**What:** Chooses the best node to run a pod.  
**Example:** Dispatcher assigning orders to available restaurants.

---

### 🔹 Controller Manager

**What:** Maintains desired state (scaling, restarts, node health).  
**Example:** Supervisor managing the kitchen staff.

---

## 🧪 Summary Table of Key Components

| Component          | Purpose                            | Real-Life Example         |
|--------------------|------------------------------------|----------------------------|
| kubectl            | CLI interface                      | Food delivery app          |
| Kubelet            | Runs containers on nodes           | Kitchen manager            |
| API Server         | Entry point for requests           | Restaurant front desk      |
| etcd               | Stores configuration/state         | Order history system       |
| Scheduler          | Assigns workloads to nodes         | Delivery dispatcher        |
| Controller Manager | Keeps desired state                | Kitchen supervisor         |

---

## 📦 Basic Kubernetes Commands

### 1️⃣ Cluster Info
```bash
kubectl cluster-info
kubectl get nodes
```

### 2️⃣ Pod Management
```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl delete pod <pod-name>
```

### 3️⃣ Deployments
```bash
kubectl create deployment myapp --image=nginx
kubectl get deployments
kubectl scale deployment myapp --replicas=5
kubectl delete deployment myapp
```

### 4️⃣ Services & Networking
```bash
kubectl expose deployment myapp --type=NodePort --port=80
kubectl get services
kubectl delete service myapp
```

### 5️⃣ ConfigMaps & Secrets
```bash
kubectl create configmap myconfig --from-literal=ENV=production
kubectl create secret generic mysecret --from-literal=DB_PASS=admin123
kubectl get configmaps
kubectl get secrets
```

---

## 🛒 Real-Life Example: E-commerce Website on K8s

Running a large-scale site like Amazon during a big sale:

- **Pods:** Serve user traffic (e.g., ordering a phone)
- **Deployments:** Ensure replicas for reliability
- **Services:** Expose app to customers
- **Autoscaling:** Handle peak traffic smoothly
- **Rolling Updates:** Deploy new features with no downtime

---

## 🧠 Final Thoughts

Kubernetes automates how apps are run, scaled, and maintained. It’s trusted by tech giants like **Google, Netflix, Amazon, and Uber** to manage massive infrastructure.

> Want to try it out? A hands-on demo of setting up a Kubernetes cluster is a great next step! 🚀
