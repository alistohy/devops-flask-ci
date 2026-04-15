# 🚀 DevOps Flask CI Project

![CI Pipeline](https://github.com/alistohy/devops-flask-ci/actions/workflows/ci.yml/badge.svg)]

## 📌 Overview

This project demonstrates a complete DevOps workflow:

* Build a Flask application
* Containerize using Docker
* Implement CI with GitHub Actions
* Push image to Docker Hub
* Deploy application on Kubernetes (k3s)

---

## 🏗️ Architecture

User → Flask App → Docker Container → Kubernetes (k3s) → Service (NodePort)

---

## 🛠️ Tech Stack

* Python (Flask)
* Docker
* GitHub Actions (CI)
* Docker Hub
* Kubernetes (k3s)

---

## 📂 Project Structure

```
devops-flask-ci/
├── app.py
├── requirements.txt
├── Dockerfile
├── test_app.py
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
├── .github/workflows/ci.yml
└── README.md
```

---

## ⚙️ CI Pipeline

The GitHub Actions pipeline performs:

1. Install dependencies
2. Run tests using pytest
3. Build Docker image

---

## 🐳 Docker

### Build Image

```
docker build -t devops-flask-ci:v1 .
```

### Run Container

```
docker run -d -p 5000:5000 devops-flask-ci
```

---

## ☸️ Kubernetes Deployment

### Apply manifests

```
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### Verify

```
kubectl get pods
kubectl get svc
```

---

## 🌐 Access Application

```
curl http://localhost:30080/
```

Health check:

```
curl http://localhost:30080/health
```

---

## 📸 Screenshots

(Add screenshots here)

---

## 👨‍💻 Author

Ali Stohy

* GitHub: https://github.com/alistohy
* LinkedIn: https://www.linkedin.com/in/ali-stohy-453792239/

---

## 🚀 Next Steps

* Implement ArgoCD (GitOps)
* Add monitoring (Prometheus & Grafana)
* Use Terraform for infrastructure
