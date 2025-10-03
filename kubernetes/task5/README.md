# Task 5 of Kubernetes

## Task Overview
Execute a rolling update for this application, integrating the nginx:1.19 image. The deployment is named nginx-deployment.

Ensure all pods are operational post-update.

## Task Implimentation
1. Check the current deployment
```bash 
kubectl get deployments

```
2. Check the container detils using
```bash 
kubectl describe deployment nginx-deployment
```
3. Perform image rolling update
```bash 
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.19
```
here container id nginx-container. use the description command to the check the image update 
4. Finally check all are running state using
```bash
kubectl get all```