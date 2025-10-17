# Day 53 of 100 daysops

## Task overview

# Fixing Nginx + PHP-FPM Pod Failure on Kubernetes

## 📘 Overview
The Nautilus DevOps team encountered an issue with the **Nginx + PHP-FPM** setup on the Kubernetes cluster.  
The Pod (`nginx-phpfpm`) stopped serving the application due to a misconfiguration in the Nginx `ConfigMap`.  
This guide documents the investigation, root cause, fix, and verification steps performed to restore functionality.

---

## 🧩 Problem Description
- The Pod **`nginx-phpfpm`** was running two containers:  
  - `php-fpm-container` (running PHP-FPM)  
  - `nginx-container` (serving static and PHP files)
- The Pod was using a `ConfigMap` named **`nginx-config`** to mount the Nginx configuration.
- Although both containers were running, the website was inaccessible from the “Website” button (port 80).

---

## 🔍 Root Cause
The `nginx.conf` file in the `nginx-config` ConfigMap had the following lines:
```nginx
listen 8099 default_server;
listen [::]:8099 default_server;
```

## Task Implemntation
1. Edit the configmap
```bash
kubectl edit configmap nginx-config

```
2. Update the lissting port 80 from 8099
```bash
listen 80 default_server;
listen [::]:80 default_server;

```

3. Recreate the pod manually as it was not created automatically
```Yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-phpfpm
  labels:
    app: php-app
spec:
  volumes:
    - name: shared-files
      emptyDir: {}
    - name: nginx-config-volume
      configMap:
        name: nginx-config
  containers:
    - name: php-fpm-container
      image: php:7.2-fpm-alpine
      volumeMounts:
        - name: shared-files
          mountPath: /var/www/html
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: nginx-config-volume
          mountPath: /etc/nginx/nginx.conf
          subPath: nginx.conf
        - name: shared-files
          mountPath: /var/www/html

```

4. Apply this manifest
```bash
kubectl apply -f nginx-phpfpm.yaml
```
5. Copy the PHP application file
```bash
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c nginx-container

```
6. Change the service port 
```bash 
kubectl edit svc nginx-service
```
make the port 80 if there are any other

After doing all these chnage the website will be visible.