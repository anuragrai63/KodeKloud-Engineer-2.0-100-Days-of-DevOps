# Day 40: Docker EXEC Operations

## Scenario

One of the Nautilus DevOps team members was working to configure services on a kkloud container that is running on App Server 2 in Stratos Datacenter. Due to some personal work he is on PTO for the rest of the week, but we need to finish his pending work ASAP. Please complete the remaining work as per details given below:

a. Install apache2 in kkloud container using apt that is running on App Server 2 in Stratos Datacenter.

b. Configure Apache to listen on port 3003 instead of default http port. Do not bind it to listen on specific IP or hostname only, i.e it should listen on localhost, 127.0.0.1, container ip, etc.

c. Make sure Apache service is up and running inside the container. Keep the container in running state at the end.

---

## Task



---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Access the container shell and install apache:

```bash
docker exec -it kkloud bash
apt update
apt install apache2 -y

```

---

### 3. Configure Apache to Listen on Port 3003 and start apache service

```bash
sed -i 's/Listen 80/Listen 3003/' /etc/apache2/ports.conf
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:3003>/' /etc/apache2/sites-available/000-default.conf
service apache2 start

```

---

### 4. Verify by curl 

```bash
curl localhost:3003
```

---

## Result

- 
