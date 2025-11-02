# Day 67 of days of devops

## MySQL Deployment on Kubernetes
# MySQL Deployment on Kubernetes

This setup deploys a MySQL database on a Kubernetes cluster using persistent storage, secrets for credentials, and a NodePort service for external access.

---

## ⚙️ Overview

**Components Created:**
1. **PersistentVolume** — `mysql-pv` (250Mi)
2. **PersistentVolumeClaim** — `mysql-pv-claim` (250Mi)
3. **Secrets:**
   - `mysql-root-pass` → Root password
   - `mysql-user-pass` → App user credentials
   - `mysql-db-url` → Database name
4. **Deployment** — `mysql-deployment`
5. **Service** — `mysql` (NodePort: 30007)

---

## 🧱 YAML Files

| File | Description |
|------|--------------|
| `mysql-pv.yaml` | Defines 250Mi PersistentVolume using `hostPath` |
| `mysql-pv-claim.yaml` | Requests 250Mi storage from PV |
| `mysql-secrets.yaml` | Stores credentials as base64-encoded secrets |
| `mysql-deployment.yaml` | Runs MySQL container with environment variables from secrets |
| `mysql-service.yaml` | Exposes MySQL via NodePort `30007` |

---
```mysql-pv.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
spec:
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  hostPath:
    path: /mnt/data/mysql

```mysql-pv-claim.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  resources:
    requests:
      storage: 250Mi

```
```mysql-secrets.yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-root-pass
type: Opaque
data:
  password: WVVJaWRoYjY2Nw==   # base64 for YUIidhb667

---
apiVersion: v1
kind: Secret
metadata:
  name: mysql-user-pass
type: Opaque
data:
  username: a29kZWtsb3VkX2pveQ==   # base64 for kodekloud_joy
  password: QnJ1Q1N0bk1UNQ==       # base64 for BruCStnMT5

---
apiVersion: v1
kind: Secret
metadata:
  name: mysql-db-url
type: Opaque
data:
  database: a29kZWtsb3VkX2RiNw==   # base64 for kodekloud_db7

```

```mysql-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        ports:
        - containerPort: 3306
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-root-pass
              key: password
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: mysql-db-url
              key: database
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: password
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim

```
```mysql-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  type: NodePort
  selector:
    app: mysql
  ports:
  - port: 3306
    targetPort: 3306
    nodePort: 30007

```

## 🧩 Deployment Steps

1. **Apply the manifests**
   ```bash
   kubectl apply -f mysql-pv.yaml
   kubectl apply -f mysql-pv-claim.yaml
   kubectl apply -f mysql-secrets.yaml
   kubectl apply -f mysql-deployment.yaml
   kubectl apply -f mysql-service.yaml

2. Check the stattus

```bash
kubectl get all
kubectl get pv
kubectl get pvc
kubectl get pods
```
