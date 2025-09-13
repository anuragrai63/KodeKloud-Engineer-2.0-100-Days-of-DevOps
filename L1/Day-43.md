# Day 42: Docker Ports Mapping

## Scenario

The Nautilus DevOps team is planning to host an application on a nginx-based container. There are number of tickets already been created for similar tasks. One of the tickets has been assigned to set up a nginx container on Application Server 2 in Stratos Datacenter. Please perform the task as per details mentioned below:


a. Pull nginx:alpine-perl docker image on Application Server 2.


b. Create a container named news using the image you pulled.


c. Map host port 6100 to container port 80. Please keep the container in running state.

---

## Task


---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Pull the nginx:alpine-perl Docker image

```bash
docker pull nginx:alpine-perl
```

---

### 3. Create a container named news using the pulled image

```bash
docker run -d --name news -p 6100:80 nginx:alpine-perl
```

---

### 4. Verify the container is running
docker ps -f name=news


## Result

