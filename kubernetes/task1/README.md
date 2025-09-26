# Kubernetes Task 1

## Task Overview
Create a pod named pod-httpd using the httpd image with the latest tag. Ensure to specify the tag as httpd:latest. Set the app label to httpd_app, and name the container as httpd-container.

## Task Implimentation
Create a file name pod-httpd.yml with below content

``` 
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
    - name: httpd-container
      image: httpd:latest

```
Save this and run the menifest

```bash
kubectl apply -f pod-httpd.yml
```

