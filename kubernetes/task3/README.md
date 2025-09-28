# Task 3 of kubernetes

## Task Overview
Create a namespace named dev and deploy a POD within it. Name the pod dev-nginx-pod and use the nginx image with the latest tag. Ensure to specify the tag as nginx:latest.

## Task implementation
1. Create Namespace
```bash
kubectl create namespace dev
```
2. Check namespace
```bash
kubectl get namespace
```

3. Run pod within the newly created namespace

```bash 
kubectl run dev-nginx-pod --image=nginx:latest --restart=Never -n dev
```
4. Verify pod in dev namespace
```bash
kubectl get pods -n dev
```