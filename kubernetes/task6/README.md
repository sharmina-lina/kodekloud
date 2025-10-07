# Task 6 of kubernetes

## Task Overview
There exists a deployment named nginx-deployment; initiate a rollback to the previous revision.
## Task Implementation
1. check the deployment using
```bash
kubectl get all
```
2. Check rollout history using
```bash 
kubectl rollout history deployment nginx-deployment
```
3. Roll back to the previous version
```bash 
kubectl rollout undo deployment nginx-deployment

```
4. Verify the rollback
```bash 
kubectl rollout status deployment nginx-deployment
```
