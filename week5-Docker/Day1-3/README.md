#  DevOps Challenge - Week 5
## Docker Fundamentals (Day 1–3)

Before containerization, the standard way to deploy applications was using virtual machines (VMs). However, VMs are resource-heavy, slow to boot, and carry complete guest operating systems. 

Docker revolutionized how applications are built, packaged, and shipped by introducing lightweight, isolated containers.

---

# Topics Covered

## 1. What is Docker & Containerization?
* Virtual Machines vs Containers.
* Advantages of containers.

## 2. Docker Architecture
* The Docker Engine (Daemon, CLI, REST API).
* Docker Images vs Containers.
* Registries (Docker Hub).

## 3. Hands-On Docker CLI
* Managing container lifecycles (`run`, `stop`, `start`, `ps`, `rm`, `exec`, `logs`).
* Inspecting containers and checking resource consumption.

## 4. Writing Your First Dockerfile
* Understanding key instructions (`FROM`, `WORKDIR`, `RUN`, `COPY`, `EXPOSE`, `CMD`, `ENTRYPOINT`, `ENV`).
* Building and running a custom Docker image.
* Pushing images to Docker Hub.

---

#  Virtual Machines vs Containers

```text
       +-----------------------+              +-----------------------+
       |   App 1   |   App 2   |              |   App 1   |   App 2   |
       +-----------+-----------+              +-----------+-----------+
       |   Bins    |   Bins    |              |   Bins    |   Bins    |
       +-----------+-----------+              +-----------+-----------+
       | Guest OS  | Guest OS  |              |    Docker Container   |
       +-----------+-----------+              +-----------------------+
       |      Hypervisor       |              |     Host OS Kernel    |
       +-----------------------+              +-----------------------+
       |     Infrastructure    |              |     Infrastructure    |
       +-----------------------+              +-----------------------+
            VIRTUAL MACHINES                         CONTAINERS
```

| Feature | Virtual Machines (VMs) | Containers (Docker) |
| :--- | :--- | :--- |
| **OS** | Full Guest OS (Gigabytes) | Shares Host OS Kernel (Megabytes) |
| **Start Time** | Minutes | Seconds |
| **Resource Efficiency** | Low (Pre-allocated RAM/CPU) | High (Dynamic usage) |
| **Isolation** | Hardware-level isolation | OS-level isolation (Namespaces/Cgroups) |

---

# Docker Architecture

Docker uses a client-server architecture:

```text
   +-------------+             +--------------+             +--------------+
   |   Client    |             | Docker Host  |             |   Registry   |
   |             |             |              |             |              |
   | docker run  | ----------> |  Docker      | <=========> |  Docker Hub  |
   | docker pull |             |   Daemon     |             |              |
   | docker build|             |  (dockerd)   |             |  Official    |
   +-------------+             +--------------+             |  Images      |
                                 /          \               +--------------+
                                v            v
                            [Images]     [Containers]
```

* **Docker Daemon (`dockerd`)**: The background service running on the host that manages Docker objects (images, containers, networks, volumes).
* **Docker Client**: The command line interface (`docker` command) used by operators to interact with the daemon.
* **Docker Image**: A read-only template used to create containers.
* **Docker Container**: A runnable instance of an image.
* **Docker Registry**: A service that stores and distributes Docker images (e.g., Docker Hub, AWS ECR).

---

#  Essential Docker Commands

## Container Lifecycle
```bash
# Run a container (pulls from Docker Hub if not present locally)
docker run -d -p 80:80 --name my-web nginx

# List running containers
docker ps

# List all containers (including stopped ones)
docker ps -a

# Stop a running container
docker stop my-web

# Start a stopped container
docker start my-web

# Remove a container
docker rm my-web

# Force remove a running container
docker rm -f my-web
```

## Debugging & Inspection
```bash
# View container logs
docker logs my-web

# Stream container logs in real time
docker logs -f my-web

# Execute a command inside a running container (e.g., open a shell)
docker exec -it my-web /bin/bash

# Inspect low-level container metadata (IP, mounts, config)
docker inspect my-web

# Monitor container resource usage (CPU, Memory)
docker stats
```

## Image Management
```bash
# List local images
docker images

# Pull an image from Docker Hub
docker pull python:3.9-slim

# Remove a local image
docker rmi python:3.9-slim
```

---

# Writing a Dockerfile

A `Dockerfile` is a text file containing instructions to build a custom Docker image. Let's build a simple Python API.

### 1. The Application Code (`app.py`)
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello DevOps! Welcome to Week 5."

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

### 2. The `Dockerfile`
Create a file named `Dockerfile` (no extension) in the same directory:

```dockerfile
# Use an official lightweight Python image as a parent image
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy dependency definition
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy all application code
COPY app.py .

# Document that the container listens on port 5000
EXPOSE 5000

# Set environment variable
ENV APP_ENV=production

# Define the command to run the application
CMD ["python", "app.py"]
```

---

# Building and Pushing Custom Images

```text
  Dockerfile --------> [ docker build ] --------> Local Image --------> [ docker push ] --------> Docker Hub
```

### 1. Build the Image
```bash
docker build -t myusername/my-python-app:1.0 .
```

### 2. Test the Image Locally
```bash
docker run -d -p 5000:5000 --name python-runner myusername/my-python-app:1.0
```
Open `http://localhost:5000` to verify the application returns "Hello DevOps!".

### 3. Push to Docker Hub
```bash
# Log in to Docker Hub registry
docker login

# Push the image
docker push myusername/my-python-app:1.0
```

---

# Learning Outcome

After completing Day 1–3, I can:

- ✅ Explain the difference between VMs and Containers
- ✅ Understand the Docker Client-Server architecture
- ✅ Pull, start, stop, monitor, and clean up containers using CLI commands
- ✅ Debug containers using `docker logs` and `docker exec`
- ✅ Write a functional custom `Dockerfile` from scratch
- ✅ Build, run, tag, and publish custom Docker images to Docker Hub

---

# Next Topics Goals

- **Docker Volumes, Networking, Compose & Best Practices (Day 4–7)**

---

# Motivation Corner

> **"If it runs on your machine, it runs in Docker. If it runs in Docker, it runs in production."**

> **"Containers abstract the OS. Kubernetes abstracts the containers. Master the container first."**

---

# Challenge Motto

```
Code the Application
         ↓
Write the Dockerfile
         ↓
Build the Container Image
         ↓
Deploy Anywhere Instantly
```
 Ship it. Run it. Scale it.
