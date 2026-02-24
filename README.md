# MEAN Stack Application – DevOps Deployment

## Project Overview

This project demonstrates containerization and cloud deployment of a full-stack MEAN (MongoDB, Express, Angular, Node.js) application using Docker, Docker Compose, GitHub Actions, Nginx, and AWS EC2.

The application is fully automated with a CI/CD pipeline that builds, pushes, and deploys updated Docker images whenever code is pushed to the main branch.

---

## Tech Stack

- MongoDB
- Express.js
- Angular
- Node.js
- Docker
- Docker Compose
- GitHub Actions
- Nginx
- AWS EC2 (Ubuntu 22.04)

---

## Architecture

```
Client → Nginx (Port 80) → Backend (Node.js + Express) → MongoDB
```

- All services run as Docker containers.
- Only port 80 is exposed publicly.
- Backend and MongoDB remain internal within the Docker network.
- Nginx acts as a reverse proxy.

---

## Repository Structure

```
frontend/
backend/
docker-compose.yaml
.github/workflows/ci-cd.yml
README.md
screenshots/
```

---


Application will be available at:

```
http://<VM_PUBLIC_IP>
```

---

## CI/CD Pipeline

CI/CD is implemented using GitHub Actions. On every push to the `main` branch:

1. Docker images for frontend and backend are built.
2. Images are pushed to Docker Hub.
3. SSH connection is made to the EC2 instance.
4. Latest images are pulled.
5. Containers are restarted using Docker Compose.

Pipeline configuration file:

```
.github/workflows/ci-cd.yml
```

---

## Cloud Deployment

- **Provider:** AWS EC2
- **OS:** Ubuntu 22.04 LTS
- **Runtime:** Docker Compose v2
- **Network:** Security group allows inbound traffic on port 80

Deployment commands executed on the server:

```bash
docker compose pull
docker compose up -d
```

---

## Nginx Reverse Proxy

- Application is accessible via port 80.
- `/` routes to the Angular frontend.
- `/api` routes to the backend service.
- Backend is not exposed publicly.

---

## MongoDB

- Official `mongo:6` Docker image used.
---

## Docker Hub Images

| Service  | Image |
|----------|-------|
| Frontend | https://hub.docker.com/repository/docker/deepakm06/frontend/ |
| Backend  | https://hub.docker.com/repository/docker/deepakm06/backend/ |