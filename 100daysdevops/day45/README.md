# Day 45 of 100 days devops journey

## Task Overview
Solve issues related to the Dokerfile
a. The Dockerfile is placed on App Server 2 under /opt/docker directory but unable to build the image using this Dockerfile.

b.Fix the issues with this file and make sure it is able to build the image.

c. Do not change base image, any other valid configuration within Dockerfile, or any of the data been used — for example, index.html.

## Task Implemntation
1. Login to the app server 2 and check the Dockerfile

2. Check the Dockerfile and found the the Apache configuration file path is wrong
the given path is 
``` /usr/local/apache2/conf.d/httpd.conf
```
but it should ne 
```bash 
/usr/local/apache2/conf/httpd.conf

```
Fixed this and rund the command 
```bash 
docker build -t httpd-image .
```
httpd-image is the name. so we can use any name here.
