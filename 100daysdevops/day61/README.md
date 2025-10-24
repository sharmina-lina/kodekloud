# Task 61 of 100 days devops

## Task Overview

## Task Implementation
1. Create a ic-deployment.yaml 
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-datacenter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-datacenter
  template:
    metadata:
      labels:
        app: ic-datacenter
    spec:
      volumes:
      - name: ic-volume-datacenter
        emptyDir: {}
      initContainers:
      - name: ic-msg-datacenter
        image: ubuntu:latest
        command: ['/bin/bash', '-c', 'echo Init Done - Welcome to xFusionCorp Industries > /ic/media']
        volumeMounts:
        - name: ic-volume-datacenter
          mountPath: /ic
      containers:
      - name: ic-main-datacenter
        image: ubuntu:latest
        command: ['/bin/bash', '-c', 'while true; do cat /ic/media; sleep 5; done']
        volumeMounts:
        - name: ic-volume-datacenter
          mountPath: /ic
```
2. Kubectl apply -f ic-deployment.yaml