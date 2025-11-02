# Redis Deployment on Kubernetes

This guide sets up a Redis instance on a Kubernetes cluster using a ConfigMap for configuration and mounted volumes for data persistence and configuration files.

---

## 🧩 Overview

We will deploy Redis with the following specifications:

- **Deployment Name:** `redis-deployment`  
- **Image:** `redis:alpine`  
- **Container Name:** `redis-container`  
- **Replicas:** `1`  
- **CPU Request:** `1 CPU`  
- **Exposed Port:** `6379`  
- **ConfigMap Name:** `my-redis-config`  
- **Config Parameter:** `maxmemory 2mb`  
- **Volumes:**
  - `data` → Mounted at `/redis-master-data` (EmptyDir)
  - `redis-config` → Mounted at `/redis-master` (ConfigMap)

---

## ⚙️ Prerequisites

- A running Kubernetes cluster  
- `kubectl` configured to access the cluster (already provided in this setup)

---

## 🧾 Step 1: Create the ConfigMap

Create a ConfigMap named `my-redis-config` with the following file:

**`my-redis-config.yaml`**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-redis-config
data:
  redis-config: |
    maxmemory 2mb


🏗️ Step 2: Create the Redis Deployment

Create a Deployment file named redis-deployment.yaml:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: redis-container
        image: redis:alpine
        ports:
        - containerPort: 6379
        resources:
          requests:
            cpu: "1"
        volumeMounts:
        - name: data
          mountPath: /redis-master-data
        - name: redis-config
          mountPath: /redis-master
          readOnly: true
      volumes:
      - name: data
        emptyDir: {}
      - name: redis-config
        configMap:
          name: my-redis-config
          items:
          - key: redis-config
            path: redis.conf

```
🔍 Step 3: Verify the Deployment

Check that the Redis pod is up and running:
```bash
kubectl get pods -l app=redis

```