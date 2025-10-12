# Task 11 of kubernetes

## Task overview
Resolve pod Deployment issue

## Task Implementation
Use the below command to check the pod details
```bash
kubectl describe pod erbserver
```
The error message says 
```
Failed to pull image "nginx:latests"
docker.io/library/nginx:latests: not found
```
so the image tag is mentioned wrongly

2. To rectify this mistake use the command 
```bash kubectl edit pod webserver
```
and change the image name nginx:latests to nginx:latest

3. Check the pod status again
```bash
kubectl get pods
```
It will show 
```
webserver   2/2     Running   0          13m
```
