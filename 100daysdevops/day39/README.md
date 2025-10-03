# Day 39 of 100 days devops practise

## Task Overview
Create an image official:xfusion from a container ubuntu_latest.

## Task Implemntation
1. Use the docker commit command to build image from the running container
```bash
docker commit ubuntu_latest official:xfusion
```
2. To check the image use the command
```bash
docker images
```