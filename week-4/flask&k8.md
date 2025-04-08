### 🚀 Overview of the `fixed-k8s.sh` Kubernetes Automation Script

The `fixed-k8s.sh` script is an end-to-end Kubernetes deployment automation tool designed to simplify the setup of a containerized application. It’s optimized for local environments like **WSL2** and development testing. While functional locally, there are important considerations when adapting it for cloud environments like **AWS EC2**.

---

### 🛠️ Script Highlights

#### 1. Project Structure & App Setup

- Creates a well-organized project directory `k8s-master-app` with folders for:
  - App code, Kubernetes manifests, configurations, logs, and helper scripts.
- Dynamically generates key files including:
  - A **Flask app (`app.py`)**
  - **Dockerfile** for containerization
  - `requirements.txt` for Python dependencies

#### 2. Kubernetes Configuration

- **Namespace**: Sets up an isolated namespace (`k8s-demo`)
- **ConfigMap & Secret**: Separates environment variables and sensitive data
- **Deployment & Service**: Ensures app replicas and exposes them via NodePort
- **Horizontal Pod Autoscaler (HPA)**: Enables automatic scaling based on CPU/memory

#### 3. Automation Scripts

- `deploy.sh`: Builds Docker image, configures Minikube, applies YAMLs
- `cleanup.sh`: Tears down all K8s resources
- `test-app.sh`: Performs a basic curl-based health check

---

### ⚠️ Challenges on AWS EC2

When attempting to run this script on an **AWS EC2** instance, several challenges emerged:

#### 🧱 1. Minikube Not Ideal on EC2

- **Problem**: EC2 is a cloud-based remote environment, whereas Minikube is best for local development.
- **Issue**: Docker driver in EC2 failed due to low CPU (less than 2 cores).
  
  **Error**:
  ```
  X Exiting due to RSRC_INSUFFICIENT_CORES: Docker has less than 2 CPUs available, but Kubernetes requires at least 2 to be available.
  ```

- **Fix**: Switch to using **Amazon EKS (Elastic Kubernetes Service)** instead of Minikube.

#### 💾 2. Insufficient Disk Space

- **Problem**: EC2’s default 8GB disk size gets filled quickly.
- **Fix**:
  - Stop EC2 instance
  - Expand the root volume in the AWS console
  - Run these commands:
    ```bash
    sudo growpart /dev/xvda 1
    sudo resize2fs /dev/xvda1
    ```

#### 🔌 3. Kubernetes Connection Issues

- **Problem**: Script assumes Minikube’s internal IP, but that doesn't apply on EC2.
  
  **Error**:
  ```
  The connection to the server 192.168.49.2:8443 was refused - did you specify the right host or port?
  ```

- **Fix**: Configure `kubectl` for your EKS cluster:
  ```bash
  aws eks update-kubeconfig --name my-cluster --region us-east-1
  ```

#### 🔒 4. Port Forwarding Doesn't Work Well

- **Problem**: `kubectl port-forward` is unreliable on EC2
- **Fix**: Use a LoadBalancer service instead of NodePort/port-forward

  **Example:**
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: k8s-master-app
    namespace: k8s-demo
  spec:
    type: LoadBalancer
    selector:
      app: k8s-master
    ports:
      - protocol: TCP
        port: 80
        targetPort: 5000
  ```

---

### ✅ Lessons Learned

- Minikube is best suited for local testing, not for cloud platforms like AWS.
- EC2’s default storage may not be sufficient for Kubernetes workloads.
- Correct `kubectl` configuration is essential when working with EKS.
- Use LoadBalancer services instead of relying on `port-forward` in production environments.

---

### 📌 Recommendations & Next Steps

- Adapt the script for **EKS deployment** rather than Minikube.
- Integrate proper disk management logic if targeting EC2.
- Use a **LoadBalancer** or Ingress Controller for external access in AWS.
