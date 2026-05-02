🚀 Taskbloom CI/CD Pipeline
This repository contains a fully automated CI/CD pipeline for the Taskbloom application, built using Jenkins, Docker, Helm, and Kubernetes, with GitHub Webhooks triggering builds on every code change.

🧩 Architecture Overview
GitHub (Push Event)
        ↓
GitHub Webhook
        ↓
Jenkins Pipeline
        ↓
Docker Build (Backend & Frontend)
        ↓
Docker Hub (Image Push)
        ↓
Helm Upgrade / Install
        ↓
Kubernetes Deployments & Services
        ↓
Ingress (NGINX)


🛠 Technology Stack

CI/CD: Jenkins Declarative Pipeline
Containerization: Docker
Container Registry: Docker Hub
Orchestration: Kubernetes
Package Manager: Helm
Ingress Controller: NGINX Ingress
Source Control: GitHub
Triggers: GitHub Webhooks


📂 Repository Structure
.
├── Jenkinsfile
├── backend/
│   ├── Dockerfile
│   └── ...
├── frontend/
│   ├── Dockerfile
│   └── ...
└── taskbloom-chart/
    ├── Chart.yaml
    ├── values.yaml
    └── templates/
        ├── backend-deployment.yaml
        ├── frontend-deployment.yaml
        ├── backend-service.yaml
        ├── frontend-service.yaml
        └── ingress.yaml


✅ CI/CD Pipeline Stages
1️⃣ Build Docker Images

Builds backend and frontend images
Tags images using Jenkins BUILD_NUMBER

Shellalisalahuddin/taskbloom-backend:<build-number>alisalahuddin/taskbloom-frontend:<build-number>Show more lines

2️⃣ Push Docker Images

Authenticates with Docker Hub using Jenkins credentials
Pushes images to Docker Hub


3️⃣ Deploy to Kubernetes with Helm

Uses Helm to install or upgrade the release
Dynamically injects image tags
Creates namespace automatically
Uses rollback on failure for safety


🧾 Jenkinsfile Highlights

Windows‑compatible (bat instead of sh)
Secure credential handling
Fully declarative pipeline
Automatic workspace cleanup
GitHub Webhook‑triggered builds


⚙️ Helm Values Structure
YAMLbackend:  image:    repository: alisalahuddin/taskbloom-backend    tag: latest  replicas: 2  service:    port: 5000frontend:  image:    repository: alisalahuddin/taskbloom-frontend    tag: latest  replicas: 2  service:    port: 80Show more lines

🌐 Kubernetes Ingress

Uses NGINX Ingress Controller
Routes traffic to the frontend service
Configurable host and path

YAMLingress:  enabled: true  className: nginx  host: taskbloom.local  path: /  pathType: PrefixShow more lines

🔔 GitHub Webhook Integration
The pipeline is automatically triggered on every push to the repository.
Webhook Configuration

Payload URL:
http://<jenkins-host>:8080/github-webhook/


Content type: application/json
Events: ✅ Push
Webhook trigger enabled in Jenkins:
GitHub hook trigger for GITScm polling




✅ Prerequisites

Jenkins (Windows or Linux)
Docker installed and running
Kubernetes cluster (Docker Desktop / Minikube / Cloud)
Helm installed
NGINX Ingress Controller installed
Docker Hub account
GitHub repository access


🚀 How It Works End‑to‑End

Developer pushes code to GitHub
GitHub sends webhook to Jenkins
Jenkins builds Docker images
Images are pushed to Docker Hub
Helm deploys the new version to Kubernetes
Ingress exposes the application

✅ Fully automated
✅ No manual steps
✅ Production‑style CI/CD

🎯 Result

✅ Continuous Integration
✅ Continuous Deployment
✅ Kubernetes‑native deployment
✅ Rollback‑safe releases
✅ Real‑world DevOps workflow


📌 Future Enhancements

✅ HTTPS via cert‑manager
✅ Blue/Green or Canary deployments
✅ Separate environments (dev/staging/prod)
✅ Monitoring with Prometheus & Grafana
✅ Secrets management


👤 Author
Ramish Ali
DevOps | Cloud | CI/CD | Kubernetes
