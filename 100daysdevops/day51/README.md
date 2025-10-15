# Day 51 of 100 days devops

## Task Overview
This guide describes the process of performing a **rolling update** on an existing Kubernetes deployment named `nginx-deployment`.  
The goal is to update the running application to use the new **nginx:1.19** image version provided by the development team.

Rolling updates ensure zero downtime by gradually replacing old Pods with new ones.

## Task implemntation
1. Verify the existing deployment
Check if the deployment exists and view current details:
```bash
kubectl get deployments
kubectl describe deployment nginx-deployment
```
2. Update the Image
``` bash 
kubectl set image deployment/nginx-deployment nginx-container =nginx:1.19

``` 
3. Verify 
```bash
kubectl rollout status deployment/nginx-deployment

```
4. It will give the message like 
```bash 
deployment "nginx-deployment" successfully rolled out
```

