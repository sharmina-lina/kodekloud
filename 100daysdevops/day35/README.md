# Task of day35 of 10daysDevOps

## Task Overview
Install docker-ce and docker compose packages and initiate docker service
## Task Implementation
1. Setup the repository 
```bash 
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```
2. Install Docker Ingine
```bash
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```

3. Start and Enable Docker
```bash
Sudo systemctl start docker
sudo systemctl enable docker
```

4. Check version and running status
```bash
docker --version
sudo systemctl status docker
```

5. Install Docker-compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.27.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

6. Check docker compose Installation
```bash
docker-compose --version```
