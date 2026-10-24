# DevOps Flask CI & GitOps Project

![CI Pipeline](https://github.com/alistohy/devops-flask-ci/actions/workflows/ci.yml/badge.svg)

## Overview

End-to-end DevOps lab project built around a lightweight Python Flask API. It covers containerization, automated testing and image builds via GitHub Actions, Kubernetes deployment on **k3s** (using both raw manifests and a custom **Helm** chart), and continuous delivery with **Argo CD**.

## Architecture

`GitHub Push` → `GitHub Actions (pytest & Docker build)` → `Docker Image` → `k3s Cluster (Manifests / Helm / Argo CD)` → `NodePort Service (:30080)`

## Tech Stack

- **Application:** Python 3.11, Flask, Pytest
- **Containerization:** Docker
- **CI Pipeline:** GitHub Actions
- **Orchestration:** Kubernetes (k3s), Helm
- **GitOps / CD:** Argo CD

## Project Structure

```text
devops-flask-ci/
├── app.py                        # Flask application (/ and /health endpoints)
├── test_app.py                   # Unit tests with pytest
├── requirements.txt              # Python dependencies
├── Dockerfile                    # Python 3.11-slim container image definition
├── .github/workflows/ci.yml      # GitHub Actions CI pipeline
├── k8s/
│   ├── deployment.yaml           # Standard Kubernetes Deployment
│   └── service.yaml              # NodePort Service (port 30080)
├── helm/flask-ci/                # Helm chart for parameterized deployment
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
└── argocd/
    └── flask-app.yaml            # Argo CD Application manifest (automated sync & self-heal)
```

## Running Locally with Docker

Build and run the container:

```bash
docker build -t alistohy/devops-flask-ci:v1 .
docker run -d -p 5000:5000 --name flask-ci alistohy/devops-flask-ci:v1
```

Test the endpoints:

```bash
curl http://localhost:5000/
curl http://localhost:5000/health
```

## Deploying to Kubernetes (k3s)

### Option 1: Standard Manifests

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl get pods,svc
```

### Option 2: Helm Chart

```bash
helm install flask-ci ./helm/flask-ci
helm list
```

### Option 3: GitOps with Argo CD

Apply the Argo CD Application manifest to sync automatically from the `main` branch (`pruned` and `selfHeal` enabled):

```bash
kubectl apply -f argocd/flask-app.yaml
```

## Verification

Once deployed on the cluster, test the `NodePort` service:

```bash
curl http://localhost:30080/
curl http://localhost:30080/health
```

## Author

**Ali Stohy**
- GitHub: [alistohy](https://github.com/alistohy)
- LinkedIn: [Ali Stohy](https://www.linkedin.com/in/ali-stohy-453792239/)
