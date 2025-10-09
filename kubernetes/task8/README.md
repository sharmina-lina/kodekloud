# Task of Kubernetes

## Task Overview
Create cornjob in kubernetes cluster
This document describes how to create and manage a Kubernetes CronJob named xfusion, which executes a simple placeholder command on a recurring schedule.
The CronJob uses an Apache HTTP Server (httpd) container and runs a dummy echo command every 10 minutes.

## Task Implementation
1. Create the CronJob Yaml
Create a manifest file /tmp/xfusion-cronjob.yml with below content
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: xfusion
spec:
  schedule: "*/10 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-xfusion
            image: httpd:latest
            command: ["echo", "Welcome to xfusioncorp!"]
          restartPolicy: OnFailure

```

2. Deploy the cronjob
```bash
kubectl appy -f /tmp/xfusion-cronjob.yml
```
3. Verify deployment
```bash
kubectl get cronjobs
```