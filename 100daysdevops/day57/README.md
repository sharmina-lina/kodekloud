🧩 Print Environment Variables in a Kubernetes Pod
📘 Overview

This task demonstrates how to create a Kubernetes Pod that prints messages using environment variables and a custom command.
The pod uses the bash image and echoes a greeting message composed of three environment variables.

⚙️ Requirements

Kubernetes cluster configured and accessible via kubectl

Proper permissions to create pods

Internet access to pull the bash image

🧱 Pod Specification

Pod Name: print-envars-greeting
Container Name: print-env-container
Image: bash
Restart Policy: Never

Environment Variables:

Variable	Value
GREETING	Welcome to
COMPANY	Nautilus
GROUP	Datacenter
Command:
```bash
["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']

```
📄 YAML Configuration

Save the following content as print-envars-greeting.yaml:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  containers:
    - name: print-env-container
      image: bash
      command: ["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']
      env:
        - name: GREETING
          value: "Welcome to"
        - name: COMPANY
          value: "Nautilus"
        - name: GROUP
          value: "Datacenter"
  restartPolicy: Never

```
🚀 Deployment Steps

1. Apply the YAML file
```bash
kubectl apply -f print-envars-greeting.yaml
```

2. Check Pod status
```bash
kubectl get pods
```
3. View the output
```bash
kubectl logs -f print-envars-greeting
```
Expected output:
```css
Welcome to Nautilus Datacenter

```
🏁 Summary

This task illustrates:

How to set environment variables inside a Kubernetes container

How to run a custom shell command using /bin/sh -c

How to use restartPolicy: Never for one-time jobs or script-based pods