Containerizing and Deploy a Next.js Apploication using Docker, GitHUb Actions and Minikube.

Overview:
This project demonstrates a complete DevOps workflow:
- Building a Next.js application
- Containerizing with Docker
- Deploying to GitHub
- Orchestrating with Kubernetes
- Verifying with port-forwarding and live pod/service checks

**Table of Contents:**
- Features
- Prerequisites
- Getting Started
- Docker Setup
- GitHub Repository
- Kubernetes Deployment
- Testing & Access
- Troubleshooting
- License

**Features**
- Next.js app containerized for portability
- Automated deployment via Git
- Kubernetes manifests for scalable deployment
- Step-by-step deployment and verification guide

**Prerequisites**
- Node.js & npm
- Docker
- Git & GitHub account
- Kubernetes cluster (Minikube, local, or cloud)
- kubectl CLI

**Getting Started**

Clone the repo:
- git clone https://github.com/kirangudupu359/my-nextjs-app.git
  cd my-nextjs-app

Install dependencies:
- npm install

Run locally:
- npm run dev

**Docker Setup**

Build Docker image:
- docker build -t my-nextjs-app .

Run container locally:
- docker run -p 3000:3000 my-nextjs-app


**GitHub Actions Workflow (CI/CD):**

This repository uses GitHub Actions for Continuous Integration and Deployment.

A typical workflow is located in .github/workflows/docker-ghcr.yml:

name: Build and Push Docker image to GHCR

on:
  push:
    branches: [ "main" ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Log in to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ghcr.io/${{ github.repository }}:latest

**How it Works**

- On every commit or PR to the main branch:
- Checks out the code
- Builds the Docker image
- Pushes the image to DockerHub (or your chosen registry)
- Can be extended to deploy to a Kubernetes cluster


**GitHub Repository**

Push all source, Dockerfile, and Kubernetes manifests to GitHub.
Remote URL: https://github.com/kirangudupu359/my-nextjs-app.git

**Kubernetes Deployment**

(Minikube)
1. Start Minikube
minikube start

2. Apply manifests
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml

3. Verify pods and services
kubectl get pods
kubectl get svc

4. Access the app

Option A (recommended):

minikube service my-nextjs-service --url
This prints a URL like http://192.168.49.2:30080

Option B (port-forward):

kubectl port-forward svc/my-nextjs-service 8080:80

Access at http://localhost:8080

Note: When running Minikube inside an AWS EC2 instance, external access requires additional networking setup (minikube tunnel, NGINX reverse proxy, or exposing NodePort via EC2 firewall). For this submission, the application is confirmed working inside Minikube.

**Deployment Notes for Reviewers**

- Pods run successfully and serve the Next.js app on port 3000.
- Kubernetes Service exposes the app via NodePort (30080).
- Verified working with kubectl port-forward and minikube service.


**Evaluation Focus Mapping**

- Docker optimization – lightweight image with proper port exposure
- GitHub Actions – automated build & push to GHCR
- Kubernetes manifests – deployment with replicas & health checks, service exposure
- Documentation – clear local run, Minikube steps, and troubleshooting notes

**Submission Details**

- GitHub Repo: https://github.com/<your-username>/<your-repo>
- GHCR Image URL: ghcr.io/<your-username>/my-nextjs-app:latest

 Done! This completes the DevOps Internship Assessment.

 Built and maintained by: Gudupu Hema Durga Kiran.

