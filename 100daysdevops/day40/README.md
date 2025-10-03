# Day 40 of 100 days devops

## Task Overview
a. Install apache2 in kkloud container using apt that is running on App Server 2 in Stratos Datacenter.


b. Configure Apache to listen on port 6200 instead of default http port. Do not bind it to listen on specific IP or hostname only, i.e it should listen on localhost, 127.0.0.1, container ip, etc.

## Task Implementation
1. Login to the container using the command 
```bash
docker exec -it kkloud bash
```

2. Update packages, list inside the containers

```bash 
apt-get update -y
```
3. Install Apache 2
```bash
apt-get install apache2 -y

```

4. Start Apache2 service
``` bash
service apache2 start 
```
5. Update apache configuration with given port 
```bash 
vi /etc/apache2/ports.conf
```
and change the port to 6200 instead of existing

6. Restart apache
```bash 
service apache2 restart
```
7. Check port 
```bash 
netstat -tulnp | grep 6200
```


