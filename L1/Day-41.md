# Day 41: Write a Docker File

## Scenario

As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file /opt/docker/Dockerfile (please keep D capital of Dockerfile) on App server 2 in Stratos DC and configure to build an image with the following requirements:

a. Use ubuntu:24.04 as the base image.

b. Install apache2 and configure it to work on 8085 port. (do not update any other Apache configuration settings like document root etc).

---

## Task



---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Create Dockerfile with below content

```bash
vi /opt/docker/Dockerfile
```
content:

FROM ubuntu:24.04
RUN apt update && \
    apt install apache2 -y && \
    sed -i 's/Listen 80/Listen 8085/' /etc/apache2/ports.conf && \
    sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8085>/' /etc/apache2/sites-available/000-default.conf
EXPOSE 8085
CMD ["apachectl", "-D", "FOREGROUND"]

---

### 3. Build the image:

```bash
cd /opt/docker
docker build -t custom_apache:8085 .
```

---

### 4. Verify image

```bash
docker image
```

---

## Result

