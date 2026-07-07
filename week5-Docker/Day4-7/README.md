#  DevOps Challenge - Week 5
## Docker Advanced (Day 4–7)

Once you understand Docker fundamentals, the next step is managing real-world production environments. This requires data persistence, container communication, orchestrating multi-container systems, and optimizing images.

---

# Topics Covered

## 1. Docker Volumes & Data Persistence
* Why containers are ephemeral.
* Bind Mounts vs Named Volumes.
* Creating and managing Docker Volumes.

## 2. Docker Networking
* Core drivers: `bridge`, `host`, `none`, `overlay`.
* Creating custom user-defined bridge networks.
* DNS and container-to-container communication.

## 3. Docker Compose
* Understanding multi-container setups.
* Writing a `docker-compose.yml` file.
* Orchestration: `docker-compose up` & `docker-compose down`.

## 4. Production Best Practices
* Multi-stage Builds for smaller images.
* Non-root security configuration.
* Optimization tips: `.dockerignore` and version pinning.

---

#  Docker Volumes & Data Persistence

By default, container filesystems are ephemeral. If a container is deleted, all modified data inside it is lost. Volumes solve this by separating the lifecycle of data from the container.

```text
               +----------------------------------------+
               |             Host Machine               |
               |                                        |
               |  [ Named Volumes ]      [ Bind Mount ] |
               |   /var/lib/docker/       /home/user/   |
               |       volumes/              app/       |
               +----------------------------------------+
                           │                     │
               Mounts to:  ▼                     ▼
                       +───────────────────────────+
                       |    Docker Container       |
                       +───────────────────────────+
```

## Types of Mounts

1. **Named Volumes**: Docker manages where the files are stored on the host filesystem. Best for general persistence (databases, uploads).
2. **Bind Mounts**: You specify the exact directory path on the host system. Best for mounting local source code into a container for real-time development.

### Volume Management CLI
```bash
# Create a named volume
docker volume create db_data

# List all volumes
docker volume ls

# Inspect a volume's host path
docker volume inspect db_data

# Remove a volume
docker volume rm db_data
```

### Mount Examples
```bash
# Mount a named volume into a database container
docker run -d --name db -v db_data:/var/lib/mysql mysql:8.0

# Mount a bind mount (local folder) for code hot-reloading
docker run -d -p 3000:3000 -v $(pwd):/app -w /app node:16-alpine npm start
```

---

# Docker Networking

Containers need to communicate with the host, other containers, and external servers.

```text
                     +---------------------------------------+
                     |         Docker Host Network           |
                     |                                       |
                     |   Container A          Container B    |
                     |   (172.18.0.2) -------> (172.18.0.3)  |
                     |        \                    /         |
                     +─────────\──────────────────/──────────+
                                v                v
                           [ Custom Bridge Network (172.18.0.1) ]
```

## Network Drivers
* **`bridge`**: The default network driver. Best for standalone container communication.
* **`host`**: Removes isolation. Container uses the host's networking stack directly (extremely fast, but no port mapping isolation).
* **`none`**: Disables all networking. Ideal for offline batch jobs.
* **`overlay`**: Enables communication between containers on different Docker hosts (Docker Swarm / cluster networks).

## Designing a Custom Bridge Network
Default bridge network does not support automatic DNS resolution by container name. Custom bridge networks do.

```bash
# Create a custom bridge network
docker network create devops-network

# List networks
docker network ls

# Run App Container on network
docker run -d --name app-service --network devops-network myapp:latest

# Run DB Container on network
docker run -d --name database-service --network devops-network redis:latest
```
Now, `app-service` can ping or connect to Redis simply using the host name `database-service` (e.g., `redis://database-service:6379`).

---

# Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It uses a single YAML file to configure all services, networks, and volumes.

### Writing `docker-compose.yml`
Here is a complete setup for a Node.js API that connects to a Redis cache:

```yaml
version: '3.8'

services:
  web-app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - REDIS_HOST=cache-service
      - REDIS_PORT=6379
    depends_on:
      - cache-service
    networks:
      - backend-net

  cache-service:
    image: redis:alpine
    ports:
      - "6379:6379"
    volumes:
      - cache_data:/data
    networks:
      - backend-net

volumes:
  cache_data:

networks:
  backend-net:
    driver: bridge
```

### CLI Workflow for Compose
```bash
# Start all services defined in docker-compose.yml in the background
docker-compose up -d

# Show current status of services
docker-compose ps

# View aggregate log stream
docker-compose logs -f

# Stop and clean up containers, networks, and images (except volumes)
docker-compose down

# Stop and clean up containers, including volumes
docker-compose down -v
```

---

# Docker Best Practices for Production

## 1. Multi-Stage Builds
Reduces final production image sizes by using a heavy image to build compilation artifacts, and copying only the compiled build files to a minimal runtime image.

```dockerfile
# Stage 1: Build the compiled binaries
FROM golang:1.18 AS builder
WORKDIR /src
COPY . .
RUN go build -o app main.go

# Stage 2: Runtime image (minimal footprint)
FROM alpine:3.15
WORKDIR /app
# Copy the compiled binary from the builder stage
COPY --from=builder /src/app .
EXPOSE 8080
CMD ["./app"]
```

## 2. Running as a Non-Root User
By default, Docker runs container processes as `root`. This poses a security risk.
```dockerfile
FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
# Use a non-privileged user already created in base node image
USER node
EXPOSE 3000
CMD ["node", "index.js"]
```

## 3. Keep Build Context Small using `.dockerignore`
Avoid copying `node_modules`, `.git`, local builds, or secret files into Docker.
Create a `.dockerignore` file:
```text
node_modules
.git
.gitignore
*.log
.env
dist
```

---

# Learning Outcome

After completing Day 4–7, I can:

- ✅ Create and mount **Docker Volumes** (Named and Bind mounts) to achieve persistence
- ✅ Use **Docker Networks** to isolate containers and support container communication
- ✅ Deploy multi-container architectures using **Docker Compose**
- ✅ Implement **Multi-stage builds** to build production-ready minimal images
- ✅ Configure non-root secure container execution
- ✅ Manage network mapping and DNS-based service discovery natively

---

# Next Topics Goals

- **AWS Cloud Administration (Week 6)**

---

# Motivation Corner

> **"A Docker container should do one thing, and do it perfectly."**

> **"Treat containers like cattle, not pets. If a container dies, spin up another one instantly."**

---

# Challenge Motto

```
Define the Infrastructure
          ↓
Compose the Services
          ↓
Volume the Data
          ↓
Launch the Whole System with One Command
```

 Multi-container deployment. Orchestrated perfectly.
