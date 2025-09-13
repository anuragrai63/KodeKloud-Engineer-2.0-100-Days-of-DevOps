# Day 44: Write a Docker Compose File

## Scenario

The Nautilus application development team has provided static website content that needs to be hosted on an `httpd` web server using a containerized platform. The team has shared the requirements with the DevOps team:

- On **App Server 2** in Stratos DC, create a container named `httpd` using a Docker Compose file located at `/opt/docker/docker-compose.yml` (use this exact file name).
- Use the `httpd` image (preferably the `latest` tag) for the container and ensure the container is named `httpd`. You may use any name for the service.
- Map port **80** of the container to port **8085** of the Docker host.
- Map the container's `/usr/local/apache2/htdocs` volume to the host's `/opt/security` directory (do not modify any data within these locations).

---

## Task

- Create a Docker Compose file to deploy an `httpd` container as described above.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Create the Docker Compose File

Create `/opt/docker/docker-compose.yml` with the following content:

```yaml
version: '3'
services:
  webserver:
    image: httpd:latest
    container_name: httpd
    ports:
      - "8085:80"
    volumes:
      - /opt/security:/usr/local/apache2/htdocs
```

---

### 3. Start the Container Using Docker Compose

```bash
cd /opt/docker
docker compose up -d
```

---

## Result

- The `httpd` container is running, serving static content on host port 8085, with the website files mapped from `/opt/security` on the host.
