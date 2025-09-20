# Docker Task

## Task Description

1. Install docker-ce and docker compose packages on App Server 1.

2. Initiate the docker service.

## Steps Performed

## Step 1: Update System

```
    sudo yum update -y
```
## Step 2:  Install Docker CE

```
sudo yum install -y yum-utils
```

# Add Docker repo
```
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```
# Install Docker CE
```
sudo yum install -y docker-ce docker-ce-cli containerd.io
```
## Install Docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" \
  -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

## Verify
```
docker --version
docker-compose --version

```
## Enable and Start Docker Service
```
    Sudo systemctl enable docker
    sudo systemctl start docker
    sudo systemctl status docker
```

