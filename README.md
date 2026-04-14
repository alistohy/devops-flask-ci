# DevOps Flask CI Project
[![CI Pipeline](https://github.com/alistohy/devops-flask-ci/actions/workflows/ci.yml/badge.svg)](https://github.com/alistohy/devops-flask-ci/actions/workflows/ci.yml)
## Kubernetes Deployment

This app is deployed on Kubernetes using k3s.

### Apply manifests
```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
