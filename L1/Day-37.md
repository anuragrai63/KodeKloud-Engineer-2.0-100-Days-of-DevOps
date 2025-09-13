# Day 37: Copy File to Docker Container

## Scenario

The Nautilus DevOps team possesses confidential data on **App Server 1** in the Stratos Datacenter. A container named `ubuntu_latest` is running on the same server.

You need to copy an encrypted file `/tmp/nautilus.txt.gpg` from the Docker host to the `ubuntu_latest` container, placing it at `/tmp/` inside the container. Ensure the file is not modified during this operation.

---

## Task

- Copy `/tmp/nautilus.txt.gpg` from the Docker host into the `/tmp/` directory of the `ubuntu_latest` container, preserving its contents.

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

### 3. Copy the File from Host to Container

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/tmp/
```

---

### 4. Verify the File Inside the Container

```bash
docker exec -it ubuntu_latest ls -l "/tmp"
```

---

## Result

- The file `/tmp/nautilus.txt.gpg` has been successfully copied to the `/tmp/` directory inside the `ubuntu_latest` container without modification.
