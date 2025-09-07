# Day 13: Securing Apache Port with iptables

## Scenario

A website is running on the Nautilus infrastructure in Stratos DC. The security team has raised a concern: Apache’s port (5004) is open to everyone due to no firewall rules being applied.  
Your task is to restrict access so that only the Load Balancer (LBR) host can reach port 5004 on all app servers.

---

## Tasks

1. **Install iptables and all its dependencies on each app host.**
2. **Block incoming port 5004 on all app servers for everyone except the LBR host.**
3. **Ensure that the firewall rules remain intact even after a system reboot.**

---

## Solution

### 1. SSH into Each App Server

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

---

### 2. Identify the LBR Host IP

Check `/etc/hosts` to get the LBR IP (for example, `stlb01`):

```bash
grep -Ei 'lb|lbr' /etc/hosts
# Example output:
# 172.16.238.14  stlb01
```

Set the LBR IP variable:

```bash
LBR_IP=172.16.238.14
```

---

### 3. Install iptables and Disable firewalld

```bash
sudo yum install -y iptables iptables-services
sudo systemctl stop firewalld 2>/dev/null || true
sudo systemctl disable firewalld 2>/dev/null || true
```

---

### 4. Enable iptables Service

```bash
sudo systemctl enable --now iptables
```

---

### 5. Configure iptables Rules

Start with a clean state for the INPUT chain:

```bash
sudo iptables -F INPUT
```

Add the following rules (replace `$LBR_IP` with your LBR host IP):

```bash
# Allow local traffic
sudo iptables -A INPUT -i lo -j ACCEPT

# Allow established and related connections
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Allow SSH (recommended to avoid lockout)
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow Apache (5004) only from the LBR host
sudo iptables -A INPUT -p tcp -s "$LBR_IP" --dport 5004 -j ACCEPT

# Drop all other incoming traffic on port 5004
sudo iptables -A INPUT -p tcp --dport 5004 -j DROP
```

---

### 6. Save Rules for Persistence

```bash
sudo service iptables save
```

---

### 7. Restart iptables

```bash
sudo systemctl restart iptables
```

---

### 8. Validation

- Ensure only the LBR host can access Apache on port 5004.
- Test by attempting to connect from other hosts and from the LBR host.

---

**Result:**  
Port 5004 is now locked down so that only the Load Balancer server can access Apache on all app servers, and the firewall rules will persist after reboot.
