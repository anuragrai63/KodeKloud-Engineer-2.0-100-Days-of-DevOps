# Day 36: Deploy Nginx Container on Application Server

## Scenario

The Nautilus DevOps team is planning to containerize several applications after a recent discussion with the application development team. To begin their testing, they need to:

- Install `docker-ce` and Docker Compose packages on **App Server 2**.
- Initiate (start and enable) the Docker service.

---

## Task

- Install Docker Community Edition (docker-ce) and Docker Compose on App Server 2.
- Start and enable the Docker service.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Pull the nginx:alpine image

```bash
docker pull nginx:alpine

```

---

### 3. Create and run the container:

```bash
docker run -d --name nginx_2 nginx:alpine

```

---

## Result

