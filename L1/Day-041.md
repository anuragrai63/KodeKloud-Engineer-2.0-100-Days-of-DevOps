# Day 41: Write a Dockerfile

## Scenario

The Nautilus application development team requires custom Docker images for their project. Some initial testing requirements have already been defined:

- Use `ubuntu:24.04` as the base image.
- Install Apache2 and configure it to listen on port `8085` (do not modify other Apache configuration settings such as the document root).

---

## Task

- Create a Dockerfile that uses `ubuntu:24.04` as the base image.
- Install Apache2 and configure it to listen on port `8085`.
- Build the Docker image and verify its presence.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Create the Dockerfile

```bash
vi /opt/docker/Dockerfile
```

**Dockerfile content:**

```dockerfile
FROM ubuntu:24.04
RUN apt update && \
    apt install apache2 -y && \
    sed -i 's/Listen 80/Listen 8085/' /etc/apache2/ports.conf && \
    sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8085>/' /etc/apache2/sites-available/000-default.conf
EXPOSE 8085
CMD ["apachectl", "-D", "FOREGROUND"]
```

---

### 3. Build the Image

```bash
cd /opt/docker
docker build -t custom_apache:8085 .
```

---

### 4. Verify the Image

```bash
docker images
```

---

## Result

- A custom Docker image named `custom_apache:8085` is created using Ubuntu 24.04 and Apache2 configured to listen on port 8085.
