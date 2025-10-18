# Task 56 of 100days devops

## 📘 Overview

This task demonstrates how to use a shared emptyDir volume between two containers in a single Kubernetes Pod.
The setup involves an Nginx web server that writes logs to a shared directory, and a sidecar container (Ubuntu) that continuously reads those logs.

🏗️ Pod Details
Component	Description
Pod Name	webserver
Volume Name	shared-logs
Volume Type	emptyDir
Container 1 (Main)	nginx-container — based on nginx:latest
Container 2 (Sidecar)	sidecar-container — based on ubuntu:latest
Shared Mount Path	/var/log/nginx
Sidecar Command	sh -c "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"
⚙️ YAML Configuration
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
    - name: shared-logs
      emptyDir: {}
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

    - name: sidecar-container
      image: ubuntu:latest
      command: ["sh", "-c", "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

🚀 Steps to Deploy

Create the Pod

kubectl apply -f webserver-pod.yaml


Check Pod Status

kubectl get pods


Describe Pod (to verify both containers are running)

kubectl describe pod webserver


Check Logs from the Sidecar Container

kubectl logs webserver -c sidecar-container -f


You should see output showing the contents of Nginx’s access and error logs every 30 seconds.

🧠 How It Works

The emptyDir volume is created when the Pod starts and is shared by all containers within that Pod.

The Nginx container writes its logs to /var/log/nginx, which resides on the shared volume.

The sidecar container periodically reads and outputs those log files, enabling real-time monitoring or further log forwarding if needed.

When the Pod is deleted, the emptyDir volume is also removed automatically.

✅ Verification

You can verify shared storage by creating a file in one container and confirming it exists in the other:

kubectl exec -it webserver -c nginx-container -- bash -c "echo 'hello world' > /var/log/nginx/test.txt"
kubectl exec -it webserver -c sidecar-container -- cat /var/log/nginx/test.txt


Expected output:

hello world

🧩 Key Takeaways

emptyDir provides ephemeral shared storage for containers in the same Pod.

Sidecar pattern is useful for log processing, monitoring, or data synchronization.

Both containers share the same file system path mounted from the volume.

Would you like me to extend the README with a short diagram (ASCII or Markdown) showing how the two containers share the volume?

⚙️ YAML Configuration
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
    - name: shared-logs
      emptyDir: {}
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

    - name: sidecar-container
      image: ubuntu:latest
      command: ["sh", "-c", "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

```
🚀 Steps to Deploy

1. Create the Pod
```yaml
kubectl apply -f webserver-pod.yaml
```
2. Check pods
```yaml

Kubectl get pods
```