# Task 47 of 100 days devops

## Task Overview
Write a dockerfile to deploy a python application

## Task Implementation
1. Create docker file name Dockerfile in the given directory with the below content
```
# Use any Python base image
FROM python:3.9

# Set the working directory
WORKDIR /app

# Copy requirements.txt from src directory
COPY src/requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application files
COPY src/ .

# Expose port 5004
EXPOSE 5004

# Run the application
CMD ["python", "server.py"]

```
2. Build image using the command
```bash 
docker build -t /python-app .
```
3. Create and run container using the build image
```bash
docker run -d --name pythonapp_nautilus -p 8096:3001 nautilus/python-app

```
4. Test the application using 
```bash 
curl http://localhost:8096

```

