# Task 2

## Task Overview
On Application Server 1 create a container named nginx_1 using the nginx image with the alpine tag. Ensure container is in a running state.

## Task Details

### Step 1
Login to the application server 1
Then run the below command to create containter named nginx_1

```docker run -d --name nginx_1 nginx:alpine
```

### step2
Check the status 
```docker ps --filter "name=nginx_1"
```

This is all about running the container and check status
