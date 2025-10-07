# Day 44 of 100days kodekloud

## Task Overview
Write a docker compose file:
- Create a docker-compose.yml file in /opt/docker/
- Define a service using the httpd image (latest)
- Name the container httpd
Map:
- Host port 8082 → Container port 80
- Host volume /opt/security → /usr/local/apache2/htdocs

## Task implementation
1. create a file with name docker-compose.yml in the given directory with the following content 
```bash
version: '3'
services:
  webserver:
    image: httpd:latest
    container_name: httpd
    ports:
      - "8082:80"
    volumes:
      - /opt/security:/usr/local/apache2/htdocs
```
2. Start the container using docker-compose
```bash
   sudo docker compose -f docker-compose.yml up -d
```
3. Then check the running container using
```bash
docker ps```