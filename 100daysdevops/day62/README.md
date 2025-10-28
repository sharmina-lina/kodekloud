# Task 62 of 100days devops
# Kubernetes Secret and Pod Deployment — Nautilus DevOps

## 📘 Overview
This project demonstrates how to securely store and use sensitive information (like license numbers or passwords) in a Kubernetes cluster using **Kubernetes Secrets**.  
The task includes creating a secret from a file and mounting it inside a running pod.

---

## 🧩 Requirements
- A running Kubernetes cluster
- `kubectl` CLI configured to access the cluster
- A file named `beta.txt` located at `/opt/beta.txt` containing the secret value (e.g., license key or password)

---

## ⚙️ Steps

### 1. Verify the secret file
Ensure the secret key file exists and view its contents:
```bash
cat /opt/beta.txt

## 2. Create the Kubernetes Secret

Create a generic secret named beta from the file:
```bash
kubectl create secret generic beta --from-file=/opt/beta.txt
```
3. Create the Pod Manifest

Create a YAML file named secret-pod.yaml with the following content:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-nautilus
spec:
  containers:
    - name: secret-container-nautilus
      image: debian:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: secret-volume
          mountPath: /opt/demo
  volumes:
    - name: secret-volume
      secret:
        secretName: beta
```
4. Deploy the menifest to create the pod
```bash
kubectl apply -f secret-pod.yaml
```
5. Verify Secret Mount Inside the Container

Access the running pod:
```bash
kubectl exec -it secret-nautilus -- bash
```
Check that the secret file is mounted correctly:
```bash
ls /opt/demo
cat /opt/demo/beta.txt

```