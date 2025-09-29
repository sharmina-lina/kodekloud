# Day 36 of 100days devops
## Task Overview
create a container named nginx_1 using the nginx image with the alpine tag. Ensure container is in a running state.
## Task Implementation

1. 
Run the below command to create containter named nginx_1

```bash 
docker run -d --name nginx_1 nginx:alpine
```

### step2
Check the status 
```docker ps --filter "name=nginx_1"
```

This is all about running the container and check status

