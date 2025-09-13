# Day 39: Create a Docker Image From Container

## Scenario

One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:


a. Create an image blog:datacenter on Application Server 2 from a container ubuntu_latest that is running on same server.

---

## Task


---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Ensure the container ubuntu_latest is running:

```bash
docker ps -f name=ubuntu_latest
```

---

### 3. Commit the container to a new image:


```bash
docker commit ubuntu_latest blog:datacenter

```

---

### 4. Verify the Images

```bash
docker images | grep blog

```

---

## Result

