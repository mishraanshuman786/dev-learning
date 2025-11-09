<p align="center">
  <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker Logo" width="120"/>
</p>

# 🐳 Docker Roadmap — Complete Topic List

---

## 🧩 1. Docker Basics
- [ ] What is Docker and why it’s used
- [ ] Containers vs Virtual Machines
- [ ] Docker architecture (Client, Daemon, Images, Containers, Registry)
- [ ] Installing Docker (Windows/Mac/Linux)
- [ ] Key terminology:
    - Image
    - Container
    - Volume
    - Network
    - Registry
    - Tag

---

## 🧱 2. Working with Docker Images
- [ ] Pulling images (`docker pull`)
- [ ] Listing images (`docker images`)
- [ ] Removing images (`docker rmi`)
- [ ] Tagging images (`docker tag`)
- [ ] Inspecting images (`docker inspect`)
- [ ] Building images (`docker build`)
- [ ] Understanding image layers & caching
- [ ] Using `.dockerignore`

---

## ⚙️ 3. Docker Containers
- [ ] Creating and running containers (`docker run`)
- [ ] Detached mode (`-d`) and interactive mode (`-it`)
- [ ] Port mapping (`-p`)
- [ ] Environment variables (`-e`)
- [ ] Executing commands inside containers (`docker exec`)
- [ ] Viewing logs (`docker logs`)
- [ ] Stopping, starting, removing containers
- [ ] Inspecting containers (`docker inspect`, `docker stats`)
- [ ] Listing running containers (`docker ps -a`)

---

## 🧾 4. Dockerfile
- [ ] Purpose of a Dockerfile
- [ ] Dockerfile instructions:
    - FROM
    - WORKDIR
    - COPY
    - RUN
    - CMD
    - ENTRYPOINT
    - EXPOSE
    - ENV
    - ARG
- [ ] Multi-stage builds
- [ ] Reducing image size (using Alpine, clearing cache)

---

## 🗂️ 5. Volumes and Data Management
- [ ] What are Docker volumes
- [ ] Bind mounts vs named volumes
- [ ] Creating and mounting volumes
- [ ] Data persistence
- [ ] Sharing volumes between containers
- [ ] Backing up and restoring volumes

---

## 🌐 6. Docker Networking
- [ ] Default bridge network
- [ ] Host and none networks
- [ ] Custom user-defined bridge networks
- [ ] Connecting containers via network
- [ ] Accessing containers by name
- [ ] Inspecting and managing networks (`docker network ls`, `docker network inspect`)

---

## 🧩 7. Docker Compose
- [ ] Purpose of `docker-compose.yml`
- [ ] YAML structure and syntax
- [ ] Defining services, ports, volumes, environment variables
- [ ] Using `depends_on`
- [ ] Using `.env` files
- [ ] Overriding commands (`command`)
- [ ] Common Docker Compose commands:
    - `docker compose up`
    - `docker compose up -d`
    - `docker compose down`
    - `docker compose ps`
    - `docker compose logs`
    - `docker compose restart`
    - `docker compose build`
- [ ] Scaling services (`docker compose up --scale`)
- [ ] Multi-file setups (`docker-compose.override.yml`)

---

## ⚡ 8. Intermediate Docker Concepts
- [ ] Healthchecks
- [ ] Restart policies (`always`, `on-failure`)
- [ ] Build args and environment variables
- [ ] Multi-container linking and dependencies
- [ ] Container lifecycle management
- [ ] Dockerfile best practices
- [ ] Debugging and inspecting logs

---

## 🚀 9. Advanced Docker Concepts
- [ ] Docker Registry and Docker Hub
- [ ] Setting up a private registry
- [ ] Pushing and pulling custom images
- [ ] Security best practices:
    - Non-root users
    - `.dockerignore`
    - Trusted base images
- [ ] Multi-stage builds for production
- [ ] Lightweight base images (Alpine)
- [ ] Resource limits (`--memory`, `--cpus`)
- [ ] Image tagging/versioning strategies
- [ ] Docker Compose for production environments

---

## ☸️ 10. Docker Swarm (Optional)
- [ ] What is Docker Swarm
- [ ] Initializing Swarm mode (`docker swarm init`)
- [ ] Deploying services (`docker service create`)
- [ ] Scaling services (`docker service scale`)
- [ ] Stack files (`docker stack deploy`)
- [ ] Rolling updates and load balancing

---

## 🧠 11. CI/CD & DevOps Integration
- [ ] Using Docker in GitHub Actions / GitLab CI / Jenkins
- [ ] Automating image builds and pushes
- [ ] Version tagging in pipelines
- [ ] Using Docker Compose for testing environments

---

## 🧰 12. Advanced & Real-World Topics
- [ ] Docker secrets and configs
- [ ] Reverse proxy setup (Nginx / Traefik)
- [ ] Logging and monitoring (Prometheus, Grafana)
- [ ] Troubleshooting and debugging containers
- [ ] Custom bridge networks in production
- [ ] Deploying containers to cloud (AWS, GCP, Render, etc.)

---

## 💻 13. Real Projects to Build
- [ ] Node.js + MongoDB app using Docker Compose
- [ ] MERN full-stack app (frontend + backend + DB)
- [ ] NestJS microservices with PostgreSQL
- [ ] CI/CD pipeline for building and pushing Docker images
- [ ] Deploy containerized app to cloud (AWS EC2, DigitalOcean, etc.)

---

## 🧑‍💻 14. Expert / Optional Topics
- [ ] Kubernetes (K8s)
- [ ] Podman / Buildah (Docker alternatives)
- [ ] Rootless Docker
- [ ] Container networking deep dive
- [ ] Image signing and verification
- [ ] Multi-platform builds

---

✅ **Goal:**  
Master Docker end-to-end — from basic containerization to production deployment with Compose, registries, and orchestration.
