# Day 40: Docker EXEC Operations

## Scenario

A Nautilus DevOps team member was configuring services within a `kkloud` container running on App Server 2 in the Stratos Datacenter. Due to their unavailability, you are required to complete the following steps:

- **Install** Apache2 inside the `kkloud` container using `apt`.
- **Configure Apache** to listen on port **3003** instead of the default HTTP port. Ensure it listens on all interfaces (not just a specific IP or hostname).
- **Ensure Apache service is running** inside the container, and the container remains up and running at the end.

---

## Task

1. Install Apache2 in the `kkloud` container.
2. Configure Apache to listen on port 3003.
3. Start Apache and verify service status.
4. Ensure the container remains running.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Access the Container Shell and Install Apache2

```bash
docker exec -it kkloud bash
apt update
apt install apache2 -y
```

---

### 3. Configure Apache to Listen on Port 3003 and Start the Service

```bash
sed -i 's/Listen 80/Listen 3003/' /etc/apache2/ports.conf
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:3003>/' /etc/apache2/sites-available/000-default.conf
service apache2 start
```

---

### 4. Verify Apache is Running on Port 3003

```bash
curl localhost:3003
```

---

## Result

- Apache2 is installed and running on port 3003 inside the `kkloud` container.
- The container remains in a running state.
