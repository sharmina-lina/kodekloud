# Task 5 of Docker

## Task Overview
# Static Website Container Fix – App Server 1

This document explains the issue resolution steps for the static website running in a Docker container named **`nautilus`** on **App Server 1**.

---

## Problem Statement

A static website hosted in a Docker container was not accessible on **host port 8080**. The container was named `nautilus` and used the `httpd` image.  

Two checks were required:

1. Verify that the container’s volume `/usr/local/apache2/htdocs` was correctly mapped to the host’s `/var/www/html`.
2. Confirm that the website was accessible at `http://localhost:8080` on App Server 1.

---

## Investigation

1. **Checked container status:**
   
   ```bash 
   docker ps -a 
   ```
2. Verified volume mapping using 

```bash 
sudo docker inspect nautilus | grep -A5 "Mounts"
```
confirmed that Source: /var/www/html -> Destination: /usr/local/apache2/htdocs

3. Check website accessability
```bash 
curl http://localhost:8080/

```
4. If not accessable, then delete the existing container
```bash
sudo docker rm < container ID >
```
5. Run a new container with correct volume and port mapping:
```bash
sudo docker run -d --name nautilus \
  -p 8080:80 \
  -v /var/www/html:/usr/local/apache2/htdocs \
  httpd
```
6. Verify container is running
```bash 
sudo docker ps
```
the expected output be like ' 0.0.0.0:8080->80/tcp' for the port.

7. Check the website accessibility again with 
```bash
curl http://localhost:8080/
```


This is all of the task

