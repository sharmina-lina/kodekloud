# Redis Deployment on Kubernetes

This task involves deploying a Redis instance on a Kubernetes cluster using a Deployment manifest. The deployment defines two volumes — one for data persistence using `emptyDir`, and another that mounts configuration data from a ConfigMap.

---

## 🧩 Task Overview

Deploy a Redis container using Kubernetes with the following specifications:
- **Image:** `redis:alpine`
- **Port:** 6379/TCP
- **Volumes:**
  - `data`: uses `emptyDir` for temporary storage
  - `config`: uses a ConfigMap for Redis configuration

---

## 🧱 Deployment YAML (Corrected Version)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deployment
  labels:
    app: redis
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
            cpu: "300m"
        volumeMounts:
        - name: config
          mountPath: /redis-master
        - name: data
          mountPath: /redis-master-data
      volumes:
      - name: data
        emptyDir: {}
      - name: config
        configMap:
          name: redis-config
          defaultMode: 420

⚙️ Create the ConfigMap

Before deploying, ensure the required ConfigMap exists:
```bash 
kubectl apply -f redis-deployment.yaml
```
2. Check pods
```bash
kubectl get pods
```

