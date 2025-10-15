# Task 13 of kubernetes

## Task overview
The Nautilus DevOps team requires a **ReplicationController** to ensure high availability for applications running on the Kubernetes cluster.  
This document outlines the steps to create and verify a ReplicationController named **`httpd-replicationcontroller`**, which manages multiple `httpd` Pods for load balancing and fault tolerance.

---


## Task Implementation
## 🧩 Specifications
- **Name:** `httpd-replicationcontroller`  
- **Image:** `httpd:latest`  
- **Container name:** `httpd-container`  
- **Replica count:** `3`  
- **Labels:**  
  - `app: httpd_app`  
  - `type: front-end`  
- **All Pods** should be in the **Running** state after deployment.

---

## ⚙️ YAML Configuration

Create a file named `httpd-replicationcontroller.yaml` with the following content:

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: httpd-replicationcontroller
  labels:
    app: httpd_app
    type: front-end
spec:
  replicas: 3
  selector:
    app: httpd_app
    type: front-end
  template:
    metadata:
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
        ports:
        - containerPort: 80
```

## Deployment steps
1. Apply the configuration
```bash 
kubectl apply -f httpd-replicationcontroller.yaml

```
2. Verify the replica controller
```bash 
kubectl get rc

```
3. Verify the running pods
```bash
kubectl get pods
```