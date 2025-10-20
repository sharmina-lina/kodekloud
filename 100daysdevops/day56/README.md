🐳 Nginx Deployment on Kubernetes
📘 Overview

This project demonstrates how to deploy a highly available and scalable static website using Nginx on a Kubernetes cluster.
It includes a Deployment with multiple replicas for load balancing and a NodePort Service for external access.
⚙️ Requirements

Kubernetes cluster configured and accessible via kubectl

Proper context set for the cluster (already done in the jump host)

Internet access to pull the nginx:latest image

🧩 Resources Created

Deployment – nginx-deployment

Image: nginx:latest

Container name: nginx-container

Replica count: 3

Port: 80

Service – nginx-service

Type: NodePort

NodePort: 30011

Exposes the Nginx application to external traffic
📄 YAML Configuration

Save the following content as nginx-deployment.yaml:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30011

```
🚀 Deployment Steps

Apply the YAML file
```bash
kubectl apply -f nginx-deployment.yaml
```
Verify resources
```bash
kubectl get all
```