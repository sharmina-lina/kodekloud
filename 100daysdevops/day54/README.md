# Task 54 of 100 days devosps

## Task Overview
This project demonstrates how to create a Kubernetes Pod with two containers that share data using a shared emptyDir volume.
Both containers use the same emptyDir volume (volume-share) mounted at different paths:

Container 1 → /tmp/news

Container 2 → /tmp/apps

Any file created by one container in the shared volume becomes immediately accessible by the other.
⚙️ Pod Specification
Pod name:
```bash
volume-share-devops
```
Containers:
| Container Name            | Image         | Mount Path | Command    |
| ------------------------- | ------------- | ---------- | ---------- |
| volume-container-devops-1 | fedora:latest | /tmp/news  | sleep 3600 |
| volume-container-devops-2 | fedora:latest | /tmp/apps  | sleep 3600 |

Shared Volume:

Name: volume-share

Type: emptyDir
🧩 YAML Configuration
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-devops
spec:
  containers:
    - name: volume-container-devops-1
      image: fedora:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/news

    - name: volume-container-devops-2
      image: fedora:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/apps

  volumes:
    - name: volume-share
      emptyDir: {}
```
🚀 Steps to Deploy and Verify

1. Apply the Pod manifest
``` bash
kubectl apply -f volume-share-devops.yaml
```
2.  Verify Pod Creation
```bash
kubectl get pods

```
3. Create a test file in the first container
```bash
kubectl exec -it volume-share-devops -c volume-container-devops-1 -- bash
echo "Shared volume test file" > /tmp/news/news.txt
```
5. Create a test file in the second container
```bash
kubectl exec -it volume-share-devops -c volume-container-devops-2 -- bash
echo "Shared volume test file" > /tmp/apps/news.txt
```
6. Verify the file in the first container
```bash
kubectl exec -it volume-share-devops -c volume-container-devops-1 -- cat /tmp/news/news.txt

```
7. Verify the file in the second container
```bash
kubectl exec -it volume-share-devops -c volume-container-devops-2 -- cat /tmp/apps/news.txt

```
