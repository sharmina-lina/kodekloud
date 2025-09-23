# Docker Task4
## Task Overview
Copy an encrypted file /tmp/nautilus.txt.gpg from the docker host to the ubuntu_latest container located at /tmp/. Ensure the file is not modified during this operation.

## Task implementation
I use docker cp commaned to copy file from a specific location to a container

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/tmp/nautilus.txt.gpg

```

I have tested the task using the below command 
``` bash
docker exec -it ubuntu_latest ls -l /tmp/
```

