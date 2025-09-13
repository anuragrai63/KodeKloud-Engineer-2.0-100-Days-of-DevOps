# Day 45: Resolve Dockerfile Issues

## Scenario

The Nautilus DevOps team is working to create new Docker images as per requirements from the development team. One of the team members is creating a Dockerfile on **App Server 3** in Stratos DC. However, the Dockerfile has issues and is not able to build the image successfully.

Your tasks:

- The Dockerfile is located on App Server 3 under `/opt/docker`.
- Fix issues with the Dockerfile so that it can successfully build the image.
- **Do not** change the base image, any other valid configuration within the Dockerfile, or any data being used (e.g., `index.html`).

> **Note:** Once the task is finished, all existing images and containers will be destroyed, and a new image will be built from your corrected Dockerfile.

---

## Task

- Review and fix the Dockerfile in `/opt/docker` on App Server 3.
- Ensure the image builds successfully without altering the base image or existing data/configurations.

---

## Solution

### 1. SSH into App Server 3

```bash
ssh banner@stapp03
```

---

### 2. Correct the Dockerfile

Update or create `/opt/docker/Dockerfile` with the following content:

```dockerfile
FROM httpd:2.4.43
RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf
RUN sed -i '/LoadModule ssl_module modules\/mod_ssl.so/s/^#//g' /usr/local/apache2/conf/httpd.conf \
    && sed -i '/LoadModule socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' /usr/local/apache2/conf/httpd.conf \
    && sed -i '/Include conf\/extra\/httpd-ssl.conf/s/^#//g' /usr/local/apache2/conf/httpd.conf

COPY certs/server.crt /usr/local/apache2/conf/server.crt
COPY certs/server.key /usr/local/apache2/conf/server.key

COPY html/index.html /usr/local/apache2/htdocs/
```

---

### 3. Build the Docker Image

```bash
cd /opt/docker
sudo docker build -t nautilus-secure-httpd .
```

---

## Result

- The Dockerfile is fixed and the image `nautilus-secure-httpd` builds successfully.
