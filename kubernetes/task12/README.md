# Task 12 of kubernetes

## Task overview
Change the configuration of deployment and services without deleting them

## Task Implementation
1. Change nordport from the port 30008 to 32165 using the command
```bash
kubectl patch service nginx-service -p '{"spec":{"ports":[{"port":80,"targetPort":80,"nodePort":32165}]}}'

```
2. check using 
```bash
kubectl get services
```
3. Increase replica from 1 to 5
```bash
kubectl scale deployment nginx-deployment --replicas=5

```
4. Check replicas of deployment
```bash
kubectl get deployment
```
5. Check the container name using 
```bash
kubectl get deployment nginx-deployment -o yaml | grep -A 5 "containers:"
```
6. update image
```bash 
kubectl set image deployment/nginx-deployment nginx-container=nginx:latest

```
nginx-container is the container name.
7. use the command from instruction 5 to check the updated image.