# Day 43: Docker Ports Mapping

## Scenario

The Nautilus DevOps team is planning to host an application inside an Nginx-based container. Several related tickets have been created, and you have been assigned the following task:

- Pull the `nginx:alpine-perl` Docker image on **Application Server 2**.
- Create a container named `news` using the image you pulled.
- Map host port **6100** to container port **80**.
- Ensure the container remains running.

---

## Task

- Pull the `nginx:alpine-perl` image.
- Create and run a container named `news`, mapping host port 6100 to container port 80.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Pull the `nginx:alpine-perl` Docker Image

```bash
docker pull nginx:alpine-perl
```

---

### 3. Create and Run the Container

```bash
docker run -d --name news -p 6100:80 nginx:alpine-perl
```

---

### 4. Verify the Container is Running

```bash
docker ps -f name=news
```

---

## Result

- The `news` container is running on App Server 2, with host port 6100 mapped to container port 80 using the `nginx:alpine-perl` image.
