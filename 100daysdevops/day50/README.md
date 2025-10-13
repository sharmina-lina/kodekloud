# Task 50 of 100dys devops

## Task overview
Create pod with specific memory and cpu limit
## Task implementation
create httpd-pod.yaml with the below content
```yaml 
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"

```

2. Run the pod apply command
```bash
kubectl apply -f httpd-pod.yaml
```
3. Check the pod running state 
```bash
kubectl get pods
```
4. check limit of pods
```bash 
kubectl describe pod httpd-pod | grep -A5 "Limits"
```