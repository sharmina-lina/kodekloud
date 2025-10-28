# Task 63 of 100days devops
## Task Overview

# 🏗️ Iron Gallery & Iron DB Deployment — Datacenter Namespace

## 📘 Overview
This project sets up a **front-end (Iron Gallery)** and a **back-end (Iron DB)** within a dedicated Kubernetes namespace.  
It demonstrates how to organize applications using **Deployments**, **Services**, and **resource limits**, along with **volume mounts** for persistent data storage.

---

## 🧩 Components Created
### 1. Namespace
- **Name:** `iron-namespace-datacenter`
- Used to isolate all Iron Gallery and Iron DB resources.

### 2. Iron Gallery Deployment
- **Name:** `iron-gallery-deployment-datacenter`
- **Labels:** `run: iron-gallery`
- **Image:** `kodekloud/irongallery:2.0`
- **Replicas:** 1
- **Container Name:** `iron-gallery-container-datacenter`
- **Resource Limits:** `100Mi` memory, `50m` CPU
- **Volume Mounts:**
  - `config` → `/usr/share/nginx/html/data` (emptyDir)
  - `images` → `/usr/share/nginx/html/uploads` (emptyDir)

### 3. Iron DB Deployment
- **Name:** `iron-db-deployment-datacenter`
- **Labels:** `db: mariadb`
- **Image:** `kodekloud/irondb:2.0`
- **Replicas:** 1
- **Container Name:** `iron-db-container-datacenter`
- **Environment Variables:**
  - `MYSQL_DATABASE=database_host`
  - `MYSQL_ROOT_PASSWORD=ComplexRootP@ss123!`
  - `MYSQL_PASSWORD=ComplexDBP@ss456!`
  - `MYSQL_USER=ironuser`
- **Volume Mount:**
  - `db` → `/var/lib/mysql` (emptyDir)

### 4. Services
#### Iron DB Service
- **Name:** `iron-db-service-datacenter`
- **Type:** `ClusterIP`
- **Selector:** `db: mariadb`
- **Ports:** `3306:3306 (TCP)`

#### Iron Gallery Service
- **Name:** `iron-gallery-service-datacenter`
- **Type:** `NodePort`
- **Selector:** `run: iron-gallery`
- **Ports:** `80:80 (TCP)`
- **NodePort:** `32678`

---

## ⚙️ Deployment Steps

### Step 1: Save the manifest
Save the following configuration as `iron-datacenter.yaml`.

```yaml
# ==========================
# Namespace
# ==========================
apiVersion: v1
kind: Namespace
metadata:
  name: iron-namespace-datacenter
---
# ==========================
# iron-gallery Deployment
# ==========================
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-gallery-deployment-datacenter
  namespace: iron-namespace-datacenter
  labels:
    run: iron-gallery
spec:
  replicas: 1
  selector:
    matchLabels:
      run: iron-gallery
  template:
    metadata:
      labels:
        run: iron-gallery
    spec:
      containers:
        - name: iron-gallery-container-datacenter
          image: kodekloud/irongallery:2.0
          resources:
            limits:
              memory: "100Mi"
              cpu: "50m"
          volumeMounts:
            - name: config
              mountPath: /usr/share/nginx/html/data
            - name: images
              mountPath: /usr/share/nginx/html/uploads
      volumes:
        - name: config
          emptyDir: {}
        - name: images
          emptyDir: {}
---
# ==========================
# iron-db Deployment
# ==========================
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-db-deployment-datacenter
  namespace: iron-namespace-datacenter
  labels:
    db: mariadb
spec:
  replicas: 1
  selector:
    matchLabels:
      db: mariadb
  template:
    metadata:
      labels:
        db: mariadb
    spec:
      containers:
        - name: iron-db-container-datacenter
          image: kodekloud/irondb:2.0
          env:
            - name: MYSQL_DATABASE
              value: database_host
            - name: MYSQL_ROOT_PASSWORD
              value: "ComplexRootP@ss123!"
            - name: MYSQL_PASSWORD
              value: "ComplexDBP@ss456!"
            - name: MYSQL_USER
              value: "ironuser"
          volumeMounts:
            - name: db
              mountPath: /var/lib/mysql
      volumes:
        - name: db
          emptyDir: {}
---
# ==========================
# iron-db Service
# ==========================
apiVersion: v1
kind: Service
metadata:
  name: iron-db-service-datacenter
  namespace: iron-namespace-datacenter
spec:
  selector:
    db: mariadb
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
  type: ClusterIP
---
# ==========================
# iron-gallery Service
# ==========================
apiVersion: v1
kind: Service
metadata:
  name: iron-gallery-service-datacenter
  namespace: iron-namespace-datacenter
spec:
  selector:
    run: iron-gallery
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 32678
  type: NodePort

```

### Step 2: Apply the manifest
```bash
kubectl apply -f iron-datacenter.yaml
