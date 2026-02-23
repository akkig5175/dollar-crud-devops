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
<img width="1470" height="956" alt="application-live1" src="https://github.com/user-attachments/assets/00b31eb9-7675-4da3-ae91-5c8537fbec00" />
<img width="1470" height="956" alt="application-live2" src="https://github.com/user-attachments/assets/76b87dbb-a213-4f50-bd7a-4b34f957012b" />
<img width="1470" height="956" alt="docker-container-running" src="https://github.com/user-attachments/assets/e1f84dca-7dce-4e67-a430-3d7c0bde048a" />
<img width="1470" height="956" alt="dockerhub-image1" src="https://github.com/user-attachments/assets/6c5d89cf-f82e-440b-a833-963f6dc16cb1" />
<img width="1470" height="956" alt="dockerhubimage2" src="https://github.com/user-attachments/assets/f8c10a9d-1319-4c6c-a00c-38b23add1024" />
<img width="1470" height="956" alt="pipeline-output-1" src="https://github.com/user-attachments/assets/5918ece1-6870-4c57-93e5-ec866e3da91f" />
<img width="1470" height="956" alt="pipeline-output-2" src="https://github.com/user-attachments/assets/930795e6-2b78-476a-ae81-7e94259b3d0b" />
<img width="1470" height="956" alt="pipeline-output-3" src="https://github.com/user-attachments/assets/d511d27e-c91b-406b-a162-95a6b594c85d" />
<img width="1470" height="956" alt="pipeline-output-4" src="https://github.com/user-attachments/assets/febb930a-fbe0-49e8-9a22-833eb1a280f2" />
<img width="1470" height="956" alt="pipeline-output-5" src="https://github.com/user-attachments/assets/0cfe1b6d-0399-4396-baa0-0d6f929f6573" />
<img width="1470" height="956" alt="instance-ss" src="https://github.com/user-attachments/assets/58d8dbb5-998a-4353-9558-e2298d8fff8f" />

