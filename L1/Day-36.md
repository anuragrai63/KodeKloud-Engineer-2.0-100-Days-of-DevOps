# Day 36: Deploy Nginx Container on Application Server

## Scenario

The Nautilus DevOps team is planning to containerize several applications following a discussion with the application development team. As part of their initial testing, they are required to:

- Deploy an **nginx** container on **App Server 2**.

---

## Task

- Pull the `nginx:alpine` Docker image.
- Run a container named `nginx_2` using this image in detached mode.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Pull the nginx:alpine Image

```bash
docker pull nginx:alpine
```

---

### 3. Create and Run the Container

```bash
docker run -d --name nginx_2 nginx:alpine
```

---

## Result

- The `nginx_2` container is running on App Server 2 using the `nginx:alpine` image.
