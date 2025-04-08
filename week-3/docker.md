# 🐳 Day-11: SRE Training – Containerization with Docker

---

## 📦 What is Containerization?

Containerization is a method of packaging an application along with its **dependencies** (libraries, configuration files, environment variables) into a **single unit** called a **container**.

✅ This ensures **consistency across environments**, from development to testing to production.

---

## 🔧 What is Docker?

Docker is an **open-source platform** that automates the **deployment**, **scaling**, and **management** of containerized applications.

---

## 🔍 Key Docker Components

| Component          | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| 🛠 Docker Engine    | Core service that builds, runs, and manages containers.                     |
| 📦 Docker Image     | Read-only template that defines the content and config of a container.      |
| 🧱 Docker Container | A running instance of a Docker image; isolated environment for apps.        |
| 📄 Dockerfile       | Script with instructions for building a Docker image.                       |
| ☁️ Docker Hub        | Cloud-based registry to store and share Docker images.                      |
| 🧬 Docker Compose    | Tool to define and run multi-container apps via `docker-compose.yml`.      |
| 💻 Docker CLI        | Command-line interface to interact with Docker Engine.                     |

---

## ⚙️ Basic Docker Workflow

1. ✍️ Write a `Dockerfile`.
2. 🧱 Build an image using `docker build`.
3. 🚀 Run a container using `docker run`.
4. 🔧 Manage images, containers, volumes, and networks.
5. ☁️ Push/pull images to/from Docker Hub.

---

## 🧰 Common Docker CLI Commands

| Command | Description |
|--------|-------------|
| `docker --version` | Show installed Docker version. |
| `docker images` | List local Docker images. |
| `docker build -t <image-name> .` | Build image from Dockerfile in current dir. |
| `docker pull <image-name>` | Pull image from Docker Hub. |
| `docker run -d -p 8080:80 <image-name>` | Run container in detached mode with port mapping. |
| `docker ps` | List running containers. |
| `docker stop <container-id>` | Stop a container. |
| `docker start <container-id>` | Start a stopped container. |
| `docker push <username>/<image-name>` | Push image to Docker Hub. |
| `docker system prune` | Clean up unused containers, images, networks, volumes. |
| `docker-compose up -d` | Start services defined in `docker-compose.yml` in detached mode. |

---

## 🔐 Authentication

- Use `docker login` to authenticate your CLI session with Docker Hub.
- First-time login requires a **Docker Access Token** for secure authentication.

---

## 🐳 Docker Compose

Docker Compose allows you to define and manage **multi-container applications** using a single **YAML file** (`docker-compose.yml`).

✅ You can define:
- Services (containers)
- Networks
- Volumes

📌 All in one config file!

---

## 🏷 Docker Image Tags

- Tags differentiate between **versions** or **configurations** of an image.
- Example: `nginx:latest`, `ubuntu:22.04`, `myapp:v1.0`

---

## 🔨 Docker Builds

- `docker build` creates an image from a Dockerfile and source code.
- Packages app + dependencies into a single image.
- **Build once, run anywhere**.

---

```diff
+ Mastered Docker fundamentals: containerization, builds, CLI usage, and multi-container orchestration!
```
