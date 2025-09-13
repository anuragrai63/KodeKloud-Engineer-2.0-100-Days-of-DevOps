# Day 39: Create a Docker Image From Container

## Scenario

A Nautilus developer has been testing new changes inside a running container. To preserve these changes, the DevOps team has been asked to create a new Docker image as a backup.

- Create an image called `blog:datacenter` on **Application Server 2** from the running container `ubuntu_latest` on the same server.

---

## Task

- Create a Docker image named `blog:datacenter` from the `ubuntu_latest` container.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Ensure the `ubuntu_latest` Container is Running

```bash
docker ps -f name=ubuntu_latest
```

---

### 3. Commit the Container to a New Image

```bash
docker commit ubuntu_latest blog:datacenter
```

---

### 4. Verify the New Image

```bash
docker images | grep blog
```

---

## Result

- The `blog:datacenter` image is successfully created from the `ubuntu_latest` container.
