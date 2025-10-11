# Taask 48 of 100 days Devops

## Task Overview
Create a pod named pod-nginx using the nginx image with the latest tag. Ensure to specify the tag as httpd:latest. Set the app label to nginx_app, and name the container as nginx-container.

## Task Implimentation
Create a file name pod-nginx.yml with below content

``` 
apiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
  labels:
    app: nginx_app
spec:
  containers:
    - name: nginx-container
      image: nginx:latest

```
Save this and run the menifest

```bash
kubectl apply -f pod-nginx.yml
```

