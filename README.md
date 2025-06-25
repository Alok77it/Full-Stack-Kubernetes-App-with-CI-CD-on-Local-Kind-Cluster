# Full Stack Kubernetes App with CI/CD on Local Kind Cluster

## 🚀 Project Overview

This project demonstrates a full stack application deployed on a local Kubernetes (Kind) cluster with a CI/CD pipeline powered by Jenkins and automated deployment using Ansible. The stack features a FastAPI backend, an NGINX frontend, and leverages containerization and multi-node orchestration for a robust local development and testing environment.

---

## 🧱 Technologies Used

| Tool              | Purpose                                      |
|-------------------|----------------------------------------------|
| Kubernetes (Kind) | Local multi-node container orchestration     |
| NGINX             | Static frontend server                       |
| FastAPI           | Python backend API                           |
| Docker            | Containerization of FastAPI app              |
| Jenkins           | CI/CD automation pipeline                    |
| Ansible           | Automated deployment & config management     |
| Shell Script      | Cluster setup, testing, automation           |
| Python            | Used in FastAPI app (functions, imports)     |

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
│   ├── services.yaml
│   ├── setup_cluster.sh      # cluster setup script is now here
│   └── test_services.sh      # service test script is now here
└── README.md
```

> **Note:** The original `scripts/` folder was removed. Scripts are now placed in their relevant directories for better organization and modularity.

---

## 🔧 Step-by-Step Setup

### ✅ Step 1: Create Multi-node Kind Cluster

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

**Shell Script:** `k8s/setup_cluster.sh`
```bash
#!/bin/bash
kind create cluster --name demo-cluster --config=k8s/kind-config.yaml
kubectl cluster-info --context kind-demo-cluster
kubectl get nodes
```

Run the script:
```bash
bash k8s/setup_cluster.sh
```

---

### ✅ Step 2: Build and Push Docker Images

1. **FastAPI Backend:**

   - Navigate to `fastapi-app/`
   - Build the Docker image:
     ```bash
     docker build -t fastapi-app:latest .
     ```
   - (Optional) Push to Docker registry if needed.

2. **NGINX Frontend:**

   - Create your NGINX Docker image as needed (customization optional).

---

### ✅ Step 3: Deploy to Kubernetes Cluster

**Kubernetes Manifests:**
- `k8s/nginx-pod.yaml` — Defines the NGINX frontend Pod.
- `k8s/fastapi-pod.yaml` — Defines the FastAPI backend Pod.
- `k8s/services.yaml` — Exposes the Pods as Kubernetes Services.

Apply manifests:
```bash
kubectl apply -f k8s/fastapi-pod.yaml
kubectl apply -f k8s/nginx-pod.yaml
kubectl apply -f k8s/services.yaml
```

---

### ✅ Step 4: Test Deployed Services

**Shell Script:** `k8s/test_services.sh`
```bash
#!/bin/bash
kubectl get pods
kubectl get services
curl http://localhost
```
Run:
```bash
bash k8s/test_services.sh
```

---

### ✅ Step 5: CI/CD With Jenkins

- Jenkins pipeline is defined in `jenkins/Jenkinsfile`.
- Jenkins automates the build, test, and deployment process.
- Integrate Jenkins with your GitHub repo and Docker registry as needed.

---

### ✅ Step 6: Automated Deployment With Ansible

- Use `ansible/deploy_k8s.yml` for automating deployments and configurations.
- Run the Ansible playbook targeting your local cluster or remote environments.

---

## 🤝 Contributing

Contributions, suggestions, and feedback are welcome!  
Please open issues or submit pull requests for new features, bug fixes, or improvements.

---

## 🚦 Project Status

> **Project is in progress.**  
> Contributions, suggestions, and feedback are welcome!

---

## 📄 License

This project is licensed under the MIT License.
