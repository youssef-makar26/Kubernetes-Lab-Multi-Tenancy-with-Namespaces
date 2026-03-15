# ☸️ Kubernetes Lab — Multi-Tenancy with Namespaces

## 📌 Overview

This project demonstrates how to implement **multi-tenancy in Kubernetes** using **Namespaces and internal service routing**.

Two isolated environments are deployed inside the same Kubernetes cluster:

* **dev environment**
* **staging environment**

Each environment contains its own:

* Backend application
* Frontend application
* Internal service (`backend-service`)

This setup ensures that each environment communicates **only with its own services**, even though they run in the same cluster.

---

# 🏗 Architecture

```
Kubernetes Cluster
│
├── Namespace: dev
│   ├── backend-pod
│   ├── backend-service
│   └── frontend-pod
│
└── Namespace: staging
    ├── backend-pod
    ├── backend-service
    └── frontend-pod
```

The frontend communicates with the backend using the internal Kubernetes DNS:

```
backend-service
```

Since the service exists inside each namespace, the routing remains isolated.

---

# 🚀 Technologies Used

* Kubernetes
* Docker
* Nginx
* Python (Backend API)
* Minikube
* kubectl

---

# 📂 Project Structure

```
K8s_Labs
│
├── Lab-3
│   ├── dev-environment.yaml
│   ├── staging-environment.yaml
│   ├── Dockerfile.backend
│   ├── Dockerfile.frontend
│   ├── backend-app.py
│   ├── nginx.conf
│   └── README.md
```

---

# ⚙️ Build Docker Images

```bash
docker build -f Dockerfile.backend -t backend-app:latest .
docker build -f Dockerfile.frontend -t frontend-app:latest .
```

If using **Minikube**:

```bash
minikube image load backend-app:latest
minikube image load frontend-app:latest
```

---

# 📦 Deploy the Environments

### Deploy DEV

```bash
kubectl apply -f dev-environment.yaml
```

### Deploy STAGING

```bash
kubectl apply -f staging-environment.yaml
```

---

# 🔎 Verify Deployment

Check **dev environment**

```bash
kubectl get pods,svc -n dev
```

Check **staging environment**

```bash
kubectl get pods,svc -n staging
```

---

# 🌐 Test the Application

Forward the frontend pod:

```bash
kubectl port-forward pod/frontend-pod 8082:80 -n dev
```

Open in browser:

```
http://localhost:8082
```

You should see the frontend communicating with the backend API.

---

# 🧪 Backend Endpoints

```
/
```

```
/info
```

```
/health
```

Each endpoint returns useful debugging information such as:

* Pod Name
* Namespace
* Service Response

---

# 📸 Screenshots

Add screenshots for:

```
kubectl get pods,svc -n dev
kubectl get pods,svc -n staging
kubectl port-forward pod/frontend-pod 8082:80 -n dev
```

---

# 🎯 Learning Outcomes

After completing this lab you will understand:

* Kubernetes **Namespaces**
* **Environment isolation**
* **ClusterIP Services**
* **Internal DNS routing**
* How frontend services communicate with backend services in Kubernetes

---

# 👨‍💻 Author

**Mohannad Khairy**

DevOps Engineer | Kubernetes | Docker | Cloud

---
