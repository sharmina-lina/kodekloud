# Task 68 of 100days devops
## 🧾  Guestbook Application Deployment**

```markdown
# Guestbook Application Deployment on Kubernetes

This repository contains Kubernetes manifests for the **Guestbook application**, which uses a Redis master-slave backend and a PHP frontend.

---

## 🏗️ Architecture Overview

The application consists of **three tiers**:

1. **Backend Tier** – Redis Master & Redis Slaves  
2. **Frontend Tier** – PHP application connecting to Redis  
3. **Services** – For internal and external communication

---

## 🧱 Components Summary

| Component | Type | Description |
|------------|------|-------------|
| `redis-master` | Deployment + Service | Single Redis master instance |
| `redis-slave` | Deployment + Service | Two Redis replicas (slaves) |
| `frontend` | Deployment + Service | PHP frontend (3 replicas) exposed via NodePort |

---

## ⚙️ Specifications

### 🧩 Redis Master
- **Deployment:** `redis-master`
- **Image:** `redis`
- **Replicas:** 1
- **Container Name:** `master-redis-nautilus`
- **Port:** 6379
- **Resources:** 100m CPU, 100Mi Memory
- **Service:** `redis-master` (ClusterIP, port 6379)

---

### 🧩 Redis Slave
- **Deployment:** `redis-slave`
- **Image:** `gcr.io/google_samples/gb-redisslave:v3`
- **Replicas:** 2
- **Container Name:** `slave-redis-nautilus`
- **Env Variable:** `GET_HOSTS_FROM=dns`
- **Port:** 6379
- **Resources:** 100m CPU, 100Mi Memory
- **Service:** `redis-slave` (ClusterIP, port 6379)

---

### 🧩 Frontend
- **Deployment:** `frontend`
- **Image:** `gcr.io/google-samples/gb-frontend@sha256:a908df8486ff66f2c4daa0d3d8a2fa09846a1fc8efd65649c0109695c7c5cbff`
- **Replicas:** 3
- **Container Name:** `php-redis-nautilus`
- **Env Variable:** `GET_HOSTS_FROM=dns`
- **Port:** 80
- **Resources:** 100m CPU, 100Mi Memory
- **Service:** `frontend` (NodePort, 30009)

---

```guestbook-app-yaml
# -----------------------------
# BACK-END TIER - REDIS MASTER
# -----------------------------
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-master
  labels:
    app: guestbook
    tier: backend
    role: master
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
      role: master
  template:
    metadata:
      labels:
        app: redis
        role: master
    spec:
      containers:
      - name: master-redis-nautilus
        image: redis
        ports:
        - containerPort: 6379
        resources:
          requests:
            cpu: "100m"
            memory: "100Mi"

---
apiVersion: v1
kind: Service
metadata:
  name: redis-master
  labels:
    app: redis
    role: master
spec:
  ports:
  - port: 6379
    targetPort: 6379
  selector:
    app: redis
    role: master

# -----------------------------
# BACK-END TIER - REDIS SLAVE
# -----------------------------
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-slave
  labels:
    app: guestbook
    tier: backend
    role: slave
spec:
  replicas: 2
  selector:
    matchLabels:
      app: redis
      role: slave
  template:
    metadata:
      labels:
        app: redis
        role: slave
    spec:
      containers:
      - name: slave-redis-nautilus
        image: gcr.io/google_samples/gb-redisslave:v3
        ports:
        - containerPort: 6379
        resources:
          requests:
            cpu: "100m"
            memory: "100Mi"
        env:
        - name: GET_HOSTS_FROM
          value: dns

---
apiVersion: v1
kind: Service
metadata:
  name: redis-slave
  labels:
    app: redis
    role: slave
spec:
  ports:
  - port: 6379
    targetPort: 6379
  selector:
    app: redis
    role: slave

# -----------------------------
# FRONT-END TIER
# -----------------------------
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: guestbook
      tier: frontend
  template:
    metadata:
      labels:
        app: guestbook
        tier: frontend
    spec:
      containers:
      - name: php-redis-nautilus
        image: gcr.io/google-samples/gb-frontend@sha256:a908df8486ff66f2c4daa0d3d8a2fa09846a1fc8efd65649c0109695c7c5cbff
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: "100m"
            memory: "100Mi"
        env:
        - name: GET_HOSTS_FROM
          value: dns

---
apiVersion: v1
kind: Service
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30009
  selector:
    app: guestbook
    tier: frontend

```

## 🚀 Deployment Instructions

1. **Apply the complete manifest**
   ```bash
   kubectl apply -f guestbook-app.yaml

2. Check and verify the deployments and services using

```bash
kubectl get all
```
wait until to run all the pods to get the app in the browser.