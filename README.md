MEAN Stack CI/CD Deployment using Docker, Jenkins & AWS

This project demonstrates end-to-end containerization and deployment of a full-stack MEAN application using Docker, Docker Compose, Jenkins CI/CD, and AWS virtual machines.

The setup automates build, push, and deployment processes using Jenkins pipelines and Docker Hub.

## Project Structure

```
mean-app/
├── backend/          # Node.js + Express API
├── frontend/         # Angular 15 Client
├── docker-compose.yml  # Multi-container setup
├── Dockerfile        # Docker build configurations
└── Jenkinsfile       # CI/CD pipeline definition
```

## Prerequisites

- Docker & Docker Compose installed
- Jenkins server running (in vm)
- AWS account with EC2 instance
- Docker Hub account

## Setup

### 1. Build Docker Images

```bash
# Build backend image
docker build -t akkig5175/dollar-backend:latest ./backend

# Build frontend image
docker build -t akkig5175/dollar-frontend:latest ./frontend
```

### 2. Push to Docker Hub

```bash
docker push akkig5175/dollar-backend:latest
docker push akkig5175/dollar-frontend:latest
```

### 3. Deploy to AWS

Ensure `docker-compose.yml` points to your Docker Hub images:

```yaml
services:
  backend:
    image: akkig5175/dollar-backend:latest

  frontend:
    image: akkig5175/dollar-frontend:latest
```

Run on your AWS EC2 instance:

```bash
cd mean-app
docker-compose up -d
```

## Jenkins Pipeline

The Jenkinsfile automates the following:

1. Clone repository
2. Build Docker images
3. Push to Docker Hub
4. Deploy to AWS via SSH

### Credentials Setup in Jenkins

- `dockerhub_cred`: Docker Hub username/password
- `HOST_IP`: AWS EC2 IP address
- `server-ssh`: SSH private key for AWS access

## Application Details

### Backend
- Node.js + Express REST API
- MongoDB integration
- CRUD operations for tutorials

### Frontend
- Angular 15 client
- HTTPClient for API communication
- Search functionality

## Access Application

Open `http://<AWS_IP>` in your browser.

##Screenshots

