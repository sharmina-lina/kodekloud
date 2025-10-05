# Day 42 of 100 days devops

## Task Overview
Createting docker network and configure it

## Task Implemntation
1. Login to the specific server
2. Create docker network using the following command 
```bash
docker network create --driver bridge --subnet 172.168.0.0/24 --ip-range 172.168.0.0/24 blog
```
3. Check the created netowrk
```bash
docker network inspect blog
```