# Day 43 of 100 days deops

## Task overview
Pull nginx:stable docker image on Application server 1, 

b. Create a container named media using the image you pulled.

c. Map host port 6400 to container port 80. Please keep the container in running state.
## Task Implementation
1. Login to the application server 1
2. pull the image
```bash 
docker pull nginx:stable
```
3. Run docker container named media, map host port 6400 to container port using 
```bash 
docker run -d --name media -p 6400:80 nginx:stable
```
4. Now check using docker ps
```bash
docker ps 
```
