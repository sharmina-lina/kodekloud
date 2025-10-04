# Day 41 of 100 days DevOps

## Task Overview
Therefore, create a docker file /opt/docker/Dockerfile (please keep D capital of Dockerfile) on App server 2 in Stratos DC and configure to build an image with the following requirements:
a. Use ubuntu:24.04 as the base image.
b. Install apache2 and configure it to work on 5001 port. (do not update any other Apache configuration settings like document root etc).

## Task Implementation
1. Login to the App server2

2. Create Dockerfile in the specific directory and write with below content

``` bash 
# Use Ubuntu 24.04 as base image
FROM ubuntu:24.04

# Install Apache2
RUN apt-get update -y && apt-get install -y apache2 && apt-get clean

# Change Apache listening port to 5001
RUN sed -i 's/Listen 80/Listen 5001/' /etc/apache2/ports.conf \
    && sed -i 's/<VirtualHost \*:80>/<VirtualHost *:5001>/' /etc/apache2/sites-available/000-default.conf

# Expose port 5001
EXPOSE 5001

# Start Apache in foreground
CMD ["apachectl", "-D", "FOREGROUND"]

```

To test:
Build image using the Dockerfile
``` bash 
cd /opt/docker
docker build -t custom-apache:latest .

```
Verify Image

```bash
docker images
```
