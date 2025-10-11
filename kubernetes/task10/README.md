# Task 10 of kubernetes 

## Task Overview
This project sets up a Kubernetes Pod named time-check within the devops namespace.
The pod continuously logs the current date and time at a configurable frequency, defined by a ConfigMap.
The output is written to a log file inside the container, simulating a simple time-based logging service.

## Task Implentation
1. Configmap: A ConfigMap named time-config stores the environment variable TIME_FREQ, which defines how often the date command runs.
```bash 
kubectl create configmap time-config --from-literal=TIME_FREQ=10 -n devops
```
2. POd Definetion
Pod Name: time-check
Namespace: devops
Container Name: time-check
Image: busybox:latest

Executes the following command in a loop:
```bash 
while true; do date >> /opt/finance/time/time-check.log; sleep $TIME_FREQ; done

```
Environment variable TIME_FREQ is loaded from the ConfigMap.

A volume named log-volume is mounted at /opt/finance/time to store log files.
Pod YAML (time-check.yaml):
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: time-check
  namespace: devops
spec:
  containers:
  - name: time-check
    image: busybox:latest
    command: ["/bin/sh", "-c"]
    args:
      - while true; do date >> /opt/finance/time/time-check.log; sleep $TIME_FREQ; done
    env:
      - name: TIME_FREQ
        valueFrom:
          configMapKeyRef:
            name: time-config
            key: TIME_FREQ
    volumeMounts:
      - name: log-volume
        mountPath: /opt/finance/time
  volumes:
    - name: log-volume
      emptyDir: {}

```
## Deployment steps:
1. Create namespace
```bash 
kubectl create namespace devops

```
2. Create configmap
```bash
kubectl create configmap time-config --from-literal=TIME_FREQ=10 -n devops

```
3. Apply the pod menifest
```bash
kubectl apply -f time-check.yaml

```
4. Verify the pod status
```bash
kubectl get pods -n devops

```
5. Check the output
```bash
kubectl exec -n devops time-check -- tail -f /opt/finance/time/time-check.log

```
This will give the time after every 10 sec