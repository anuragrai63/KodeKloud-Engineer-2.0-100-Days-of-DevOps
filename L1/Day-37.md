# Day 37: Copy File to Docker Container

## Scenario

The Nautilus DevOps team possesses confidential data on App Server 1 in the Stratos Datacenter. A container named ubuntu_latest is running on the same server.

Copy an encrypted file /tmp/nautilus.txt.gpg from the docker host to the ubuntu_latest container located at /tmp/. Ensure the file is not modified during this operatio

## Task


---

## Solution

### 1. SSH into App Server 1

```bash
ssh tony@stapp01
```

---

### 2. Check Container Status 

```bash
docker ps -a
```

---

### 3. Copy file from machine to Container

```bash
docker cp /tmp/nautilus.txt.gpg  ubuntu_latest:/tmp/
```

### 3. verify file

```bash
docker exec -i -t  ubuntu_latest ls -l "/tmp"
```

---

## Result

