
# Kubernetes Deployment - Multi-Component Chat Application

This repository contains Kubernetes manifests and Dockerfiles used to deploy a full-stack chat application with the following components:

## 📦 Components

### 1. `ostad-ui` (Frontend)
- **Tech**: Vite + React
- **Description**: Provides the student registration form and student list UI.
- **Port**: 5173 inside container, served on 80 via `serve`
- **Dockerfile**: Builds static files and serves via `serve`

### 2. `ostad-server` (Backend)
- **Tech**: Node.js + Express + MongoDB driver
- **Description**: Handles API endpoints `/addStudent` and `/getStudents`.
- **Port**: 5050

### 3. `mongo` (Database)
- **Tech**: MongoDB
- **Description**: Stores student data in `ostad_db.students`
- **Port**: 27017

### 4. `mongo-express` (Admin Panel)
- **Tech**: mongo-express
- **Description**: Web-based interface to interact with MongoDB
- **Port**: 8081

---

## 🧪 How to Deploy

### 1. Create Namespace
```bash
kubectl create namespace sady
```

### 2. Apply Secrets (optional)
```bash
kubectl apply -f mongo-secret.yaml
```

### 3. Apply Deployments and Services
```bash
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-service.yaml

kubectl apply -f mongo-express-deployment.yaml
kubectl apply -f mongo-express-service.yaml

kubectl apply -f ostad-server-deployment.yaml
kubectl apply -f ostad-server-service.yaml

kubectl apply -f ostad-ui-deployment.yaml
kubectl apply -f ostad-ui-service.yaml
```

### 4. Apply Ingress
```bash
kubectl apply -f ingress.yaml
```

Make sure Ingress controller is installed:
```bash
minikube addons enable ingress
minikube tunnel
```

### 5. Update /etc/hosts (on your host machine)
```
127.0.0.1 chat.local
127.0.0.1 mongo.local
```

---

## ✅ Features Tested

- [x] `chat.local` serves frontend
- [x] `mongo.local` opens Mongo Express UI
- [x] Add student and view student list
- [x] MongoDB auth with `MONGO_URL` and admin credentials
- [x] Ingress routes confirmed working with `ingressClassName: nginx`

---

## 🔐 Bonus

- CPU & Memory limits configured in deployments
- Secrets used for MongoDB credentials
- Persistent Volume optional

---

## 📎 License
This project is for academic deployment and DevOps training purposes.
