---
title: docker常用命令
date: 2020-07-01 12:53:24
tags: docker
---

## docker command help
```bash
docker command --help
```
![1](1.jpg)
## use images
### list images
```bash
docker images
```
![2](2.jpg)
### start container by image
```bash 
docker run -t -i ubuntu:16.04 /bin/bash
```
![3](3.jpg)
### search images
```bash 
docker search mysql
```
![5](5.jpg)
### get new images
```bash
docker pull ubuntu:18.04
```
![4](4.jpg)
### delete image
```bash
docker rmi ubuntu:18.04
```
![6](6.jpg)
### **[more operations][https://www.runoob.com/docker/docker-image-usage.html] **

## use container
### start container
```bash
docker run -t -i ubuntu:16.04 /bin/bash ## -d background
```
### show containers
```bash
docker ps -a 
```
![7](7.jpg)

### stop & start & restart container
```bash
docker start container_id ## RUN IN THE BACKGROUND
docker stop container_id
docker restart container_id
```
### enter container
```bash
docker attach container_id ## use exit will stop container
```

```bash
docker exec -it container_id /bin/bash  ## use exit will not stop container
```

### export container

```bash
docker export container_id > container.tar
```
### import container_snap to image
```bash
cat docker/mysql.tar | docker import - mysql:v1
```
![8](9.jpg)

### delete container 
```bash 
docker rm -f container_id
```

### show container's port mapping
```bash
docker port container_id
```
![9](9.jpg)

### connect container by port mapping
```bash
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD = 123456 mysql 
```
## connect containers
### create a docker network
```bash
docker network create -d bridge hadoop-net
```
### show networks
```bash
docker network ls
```
### run a container and connect to the network
```bash
docker run -itd --name hadoop1 --network hadoop-net ubuntu /bin/bash
```