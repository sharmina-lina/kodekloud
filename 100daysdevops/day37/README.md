# Day 37 of 100 days Devops

## Task overview
Copy an encrypted file /tmp/nautilus.txt.gpg from the docker host to the ubuntu_latest container located at /tmp/

## Task Implementation

1. Use docker cp commaned to copy file from a specific location to a container

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/tmp/nautilus.txt.gpg

```
2. 
I have tested the task using the below command 
``` bash
docker exec -it ubuntu_latest ls -l /tmp/
```
