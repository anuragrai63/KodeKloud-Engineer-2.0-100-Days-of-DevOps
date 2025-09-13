# Day 42: Create a Docker Network

## Scenario

The Nautilus DevOps team needs to set up several docker environments for different applications. One of the team members has been assigned a ticket where he has been asked to create some docker networks to be used later. Complete the task based on the following ticket description:

a. Create a docker network named as ecommerce on App Server 3 in Stratos DC.

b. Configure it to use macvlan drivers.

c. Set it to use subnet 172.28.0.0/24 and iprange 172.28.0.0/24.

---

## Task


---

## Solution

### 1. SSH into App Server 3

```bash
ssh banner@stapp03
```

---

### 2. Create the macvlan network:

```bash
docker network create \
  -d macvlan \
  --subnet=172.28.0.0/24 \
  --ip-range=172.28.0.0/24 \
  --gateway=172.28.0.1 \
  -o parent=eth0 \
  ecommerce

```



---

### 3. Verify the Network

```bash
docker network inspect ecommerce

```

---



## Result

