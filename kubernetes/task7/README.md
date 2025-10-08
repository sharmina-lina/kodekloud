# Task 7 of kubernetes

## Task Overview
Deploy replica set in kubernetes cluster:
Create a ReplicaSet using nginx image with latest tag (ensure to specify as nginx:latest) and name it nginx-replicaset.

Apply labels: app as nginx_app, type as front-end.

Name the container nginx-container. Ensure the replica count is 4.

## Task Implemntation
create a nginx-replicaset.yaml with the below content
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
  labels:
    app: nginx_app
    type: front-end
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nginx_app
      type: front-end
  template:
    metadata:
      labels:
        app: nginx_app
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80

```
save the file and run the below command to create the replica:
```bash 
kubectl create -f nginx-replicaset.yaml
```
check with the command 
```bash
kubectl get all
```
