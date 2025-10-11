# Task 9 of kubernetes Kluster

## Task Overview

## Task Implementation

2. create a yaml file 
```bash
vi countdown-datacenter.yaml
```
with content 
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-datacenter
spec:
  template:
    metadata:
      name: countdown-datacenter
    spec:
      containers:
      - name: container-countdown-datacenter
        image: debian:latest
        command: ["sleep", "5"]
      restartPolicy: Never

```
2. create the job 
```bash
kubectl apply -f countdown-datacenter.yaml

```


