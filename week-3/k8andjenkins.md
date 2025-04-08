# 📌 Kubernetes and Jenkins Deployment Project

## Project 1: Mini Kubernetes Demo (Manual Deployment, No Jenkins)

### 📝 Overview

This project showcases how to deploy a **Python Flask application** inside a **Kubernetes cluster using Minikube**. The primary goal is to containerize the app and manually deploy it using Kubernetes resources like **Deployments**, **Services**, **ConfigMaps**, and **Namespaces**. Jenkins is not used here—all steps are performed manually.

---

### 📁 Project Structure

```
mini-k8s-demo/
│── app/
│   ├── app.py               # Flask Application
│   ├── requirements.txt     # App Dependencies
│   ├── Dockerfile           # Docker Image Setup
│── k8s/
│   ├── namespace.yaml       # Defines Kubernetes Namespace
│   ├── configmap.yaml       # App Configuration via ConfigMap
│   ├── deployment.yaml      # Kubernetes Deployment
│   ├── service.yaml         # Kubernetes Service
│── deploy.sh                # Deployment Automation Script
│── troubleshoot.sh          # Basic Troubleshooting Script
│── k8s-explained.md         # Kubernetes Concepts Explained
```

---

### 🔧 Key Steps & Learnings

#### 1️. Dockerizing the Flask App

- Built a basic Flask API with three routes:
  - `/` → Returns pod/service metadata.
  - `/api/info` → Returns app version/name.
  - `/api/health` → Health probe endpoint.
- Declared dependencies in `requirements.txt`.
- Wrote the Dockerfile:

```Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py .
EXPOSE 5000
CMD ["python", "app.py"]
```

**Key Points:**
- Lightweight base image.
- Uses pip to install required libraries.
- Exposes port 5000 for Kubernetes service routing.

---

#### 2️. Writing Kubernetes YAMLs

**Namespace (namespace.yaml)**

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: mini-demo
```

**ConfigMap (configmap.yaml)**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: mini-demo
data:
  APP_NAME: "Kubernetes Mini Demo"
  APP_VERSION: "1.0.0"
```

**Deployment (deployment.yaml)**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: flask-app
  namespace: mini-demo
spec:
  replicas: 2
  selector:
    matchLabels:
      app: flask-app
  template:
    metadata:
      labels:
        app: flask-app
    spec:
      containers:
        - name: flask-app
          image: mini-k8s-demo:latest
          imagePullPolicy: Never
          ports:
            - containerPort: 5000
          envFrom:
            - configMapRef:
                name: app-config
```

**Service (service.yaml)**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: flask-service
  namespace: mini-demo
spec:
  type: NodePort
  selector:
    app: flask-app
  ports:
    - port: 80
      targetPort: 5000
      nodePort: 30080
```

---

#### 3️. Automating with `deploy.sh`

```bash
#!/bin/bash
set -e

echo "🚀 Starting Minikube..."
minikube start --driver=docker

echo "🐳 Setting up Docker..."
eval $(minikube docker-env)

echo "🛠️ Building Docker Image..."
docker build -t mini-k8s-demo:latest app/

echo "📌 Deploying to Kubernetes..."
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml

echo "✅ Deployment complete! Access the app using:"
minikube service flask-service -n mini-demo --url
```

---

#### 4️. Troubleshooting with `troubleshoot.sh`

```bash
#!/bin/bash

echo "🔍 Checking Minikube Status..."
minikube status

echo "🛠️ Checking Kubernetes Resources..."
kubectl get pods -n mini-demo
kubectl get services -n mini-demo
kubectl logs -l app=flask-app -n mini-demo

# If a pod is stuck
kubectl describe pod <pod-name> -n mini-demo
kubectl logs <pod-name> -n mini-demo

# If Minikube is down
minikube stop && minikube delete
minikube start --driver=docker
```

---

### ✅ Final Result

To deploy the app:

```bash
chmod +x deploy.sh
./deploy.sh
```

The Flask app will be live inside a Minikube-powered Kubernetes cluster!

---

## Project 2: CI/CD Pipeline with Jenkins + Kubernetes

### 📝 Overview

This project expands on the previous one by adding **CI/CD automation using Jenkins**. It automates every step—from code fetch to Kubernetes deployment—whenever code is pushed to GitHub. Jenkins handles:

- ✅ Cloning the GitHub repo
- ✅ Building the Docker image
- ✅ Deploying Kubernetes manifests
- ✅ Confirming rollout status

---

### 📁 Project Structure

```
my-k8s-app/
│── app/
│   ├── app.py
│   ├── requirements.txt
│   ├── Dockerfile
│── k8s/
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── deployment.yaml
│   ├── service.yaml
│── deploy.sh
│── jenkinsfile
│── troubleshoot.sh
```

---

### ⚙️ Jenkins Setup

1. Install Jenkins:
```bash
sudo apt update && sudo apt install -y openjdk-11-jdk
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
echo "deb http://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list
sudo apt update
sudo apt install -y jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

2. Open Jenkins at `http://localhost:8080` and set up admin credentials.
3. Install required plugins: Git, Docker, and Pipeline.
4. Generate SSH keys for GitHub deploy access:

```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
cat ~/.ssh/id_rsa.pub  # Add this to GitHub -> Deploy Keys
```

5. Create a Jenkins Pipeline and connect to the GitHub repo.

---

### 🧾 Jenkinsfile (Pipeline Code)

```groovy
pipeline {
  agent any
  environment {
    REPO_URL = "git@github.com:Tamanna247/kubernetes_with_jenkins.git"
    WORKDIR = "${WORKSPACE}/my-k8s-app"
    VENV_PATH = "${WORKSPACE}/venv"
    DOCKER_IMAGE = "my-k8s-app:latest"
    K8S_NAMESPACE = "demo-namespace"
  }
  stages {
    stage('Clone Repository') {
      steps {
        cleanWs()
        sh '''
          echo "Cloning repository..."
          [ -d "$WORKDIR" ] && rm -rf "$WORKDIR"
          git clone $REPO_URL "$WORKDIR"
          echo "Repository cloned!"
          ls -la "$WORKDIR"
        '''
      }
    }
    stage('Setup Python Environment') {
      steps {
        sh '''
          python3 -m venv "$VENV_PATH"
          . "$VENV_PATH/bin/activate"
          pip install --upgrade pip build pytest
        '''
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          echo 'Building Docker Image...'
          sh 'cd my-k8s-app/app && docker build -t my-k8s-app:latest .'
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
        sh '''
          kubectl apply -f "$WORKDIR/k8s/namespace.yaml"
          kubectl apply -f "$WORKDIR/k8s/configmap.yaml"
          kubectl apply -f "$WORKDIR/k8s/deployment.yaml"
          kubectl apply -f "$WORKDIR/k8s/service.yaml"
          kubectl -n $K8S_NAMESPACE rollout status deployment/flask-app
        '''
      }
    }
  }
  post {
    success {
      echo '✅ Deployment successful!'
    }
    failure {
      echo '❌ Pipeline failed. Check logs.'
    }
  }
}
```

---

### 🚑 Common Jenkins Issues & Fixes

- **🔴 Repo clone failed:** Add correct SSH keys to GitHub deploy keys.
- **🔴 Minikube not starting:** Ensure Docker driver is used.
  ```bash
  minikube start --driver=docker
  ```
- **🔴 Namespace errors:** Verify that namespace names match across files.
- **🔴 Rollout status failing:** Tune readiness/liveness probes to allow more time.

---

### 🧰 Manual Deploy with `deploy.sh` (Optional)

```bash
#!/bin/bash
set -e

echo "🚀 Starting Kubernetes Deployment..."

if ! minikube status | grep -q "host: Running"; then
  echo "🔄 Starting Minikube..."
  minikube start
else
  echo "✅ Minikube is already running."
fi

eval $(minikube docker-env)

echo "🐳 Building Docker Image..."
cd app && docker build -t my-k8s-app:latest . && cd ..

echo "🛠 Applying Kubernetes resources..."
kubectl apply -f k8s/
kubectl -n demo-namespace rollout status deployment/flask-app

echo "🔗 Access application at:"
minikube service flask-service -n demo-namespace --url
```

---

### ✅ Final Outcome

Once configured, Jenkins will automatically:

1. Pull latest code from GitHub
2. Build the Docker image
3. Deploy the app into Kubernetes
4. Confirm successful deployment

This CI/CD setup minimizes manual steps and accelerates deployment!

