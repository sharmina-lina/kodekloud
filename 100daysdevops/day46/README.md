# Task 46 of 100days devops

## Task Overview
Deploy application on docker container
This project sets up a containerized LAMP-style stack (PHP + MariaDB) using Docker Compose on App Server 3 in the Stratos Datacenter.
It allows the team to test the web application before the live deployment.

## Task Implementation
1. Create directory if not already created
```bash
sudo mkdir -p /opt/security
```
2. created and updated the docker compose file:
``` sudo vi /opt/security/docker-compose.yml
```
with the content
```yml
version: '3.8'

services:
  web:
    container_name: php_web
    image: php:apache
    ports:
      - "8085:80"
    volumes:
      - /var/www/html:/var/www/html
    depends_on:
      - db

  db:
    container_name: mysql_web
    image: mariadb:latest
    ports:
      - "3306:3306"
    volumes:
      - /var/lib/mysql:/var/lib/mysql
    environment:
      MYSQL_DATABASE: database_web
      MYSQL_USER: webuser
      MYSQL_PASSWORD: Str@t0sP@ss#2025
      MYSQL_ROOT_PASSWORD: Root@Temp#123

```
3. Deploy the stack
```bash
cd /opt/security
sudo docker compose up -d
```
4. verify running containers:
```bash
docker ps
```
see two container name php_web and mysql_db is up and running
5. Access the web service
```bash
sudo curl http://<APP server IP >: 8085
```
here APP server IP is the IP of webserver IP.
This is all of the task
