# Full Stack Kubernetes App with CI/CD on Local Kind Cluster

## 🚀 Project Overview

This project demonstrates a full stack application deployed on a local Kubernetes (Kind) cluster with a CI/CD pipeline powered by Jenkins and automated deployment using Ansible. The stack features a FastAPI backend, an NGINX frontend, and leverages containerization and multi-node orchestration for a robust local development and testing environment.

---

## 🧱 Technologies Used

| Tool        | Purpose                                 |
|-------------|-----------------------------------------|
| Kubernetes (Kind) | Local multi-node container orchestration |
| NGINX       | Static frontend server                  |
| FastAPI     | Python backend API                      |
| Docker      | Containerization of FastAPI app         |
| Jenkins     | CI/CD automation pipeline               |
| Ansible     | Automated deployment & config mgmt      |
| Shell Script| Cluster setup, testing, automation      |
| Python      | Used in FastAPI app (functions, imports)|

---

## 📁 Folder Structure

```
fullstack-k8s-project/
├── jenkins/
│   └── Jenkinsfile
├── ansible/
│   └── deploy_k8s.yml
├── fastapi-app/
│   ├── main.py
│   └── Dockerfile
├── k8s/
│   ├── kind-config.yaml
│   ├── nginx-pod.yaml
│   ├── fastapi-pod.yaml
│   └── services.yaml
├── scripts/
│   ├── setup_cluster.sh
│   └── test_services.sh
└── README.md
```
---

## 🔧 Step-by-Step Setup

### ✅ Step 1: Multi-node Kind Cluster

**Config:** `k8s/kind-config.yaml`
```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
    image: kindest/node:v1.29.2
  - role: worker
    image: kindest/node:v1.29.2
  - role: worker
    image: kindest/node:v1.29.2
    extraPortMappings:
      - containerPort: 80
        hostPort: 80
        protocol: TCP
```

**Shell Script:** `scripts/setup_cluster.sh`
```bash
#!/bin/bash
kind create cluster --name demo-cluster --config=k8s/kind-config.yaml
kubectl cluster-info --context kind-demo-cluster
kubectl get nodes
```

---

## 🚦 Project Status

> **Project is in progress.**  
> Contributions, suggestions, and feedback are welcome!

---

## 📄 License

This project is licensed under the MIT License.

