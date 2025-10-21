📊 Grafana Deployment on Kubernetes
📘 Overview

This task demonstrates how to deploy a Grafana application on a Kubernetes cluster using a Deployment and expose it using a NodePort Service.
Once deployed, the Grafana login page should be accessible externally through the assigned NodePort — no further configuration inside Grafana is required.

⚙️ Task Requirements

Create a Deployment

Name: grafana-deployment-xfusion

Image: Any Grafana image (used: grafana/grafana:latest)

Replica count: 1 (can be scaled as needed)

Container port: 3000

Create a Service

Type: NodePort

Name: grafana-service

NodePort: 32000

Purpose: Expose the Grafana app externally

📄 YAML Configuration

Save the following as grafana-deployment.yaml:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-xfusion
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana-container
          image: grafana/grafana:latest
          ports:
            - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: grafana-service
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 32000

```

🚀 Deployment Steps

1. Apply the configuration
```bash
kubectl apply -f grafana-deployment.yaml
```
2. Verify the deployment
```bash
kubectl get all
```