# Task 64 of 100days devops

## Task Overview
# 🐍 Python Flask App Deployment — DevOps Kubernetes Fix

## 📘 Overview
This task involved troubleshooting and fixing a misconfigured Kubernetes deployment for a **Python Flask web application**.  
The application was deployed successfully but was initially **not accessible** due to an incorrect service configuration and an invalid image reference.  
After the fixes, the Flask app is running and reachable on the specified NodePort.

---

## 🧩 Components Overview
| Resource Type | Name | Description |
|----------------|------|-------------|
| **Deployment** | `python-deployment-devops` | Deploys the Python Flask container |
| **Service** | `python-service-devops` | Exposes the Flask app externally using NodePort |
| **Pod** | `python-deployment-devops-7859694dcf-z4jh6` | Running instance of the Flask application |

---

## ⚙️ Fix Summary

### 🧠 Problem 1: Invalid Image
The image name was wrongly mentioned in both pod and deployment configuration. Rectify image name from pod and deployment configuration.

### 🧠 Problem 2: Invalid Port
The service port: 8080 and targetPort: 8080
nodePort: 32345 but this is a flax app that port and target Port is 5000.
So edit the service configuration and make the port and target port 5000 instead of 8080.


