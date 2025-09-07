# Day 12: Troubleshooting Apache Service on Custom Port

## Scenario

The monitoring tool has reported an issue in the Stratos Datacenter:  
One of the app servers (App Server 1) has an issue—its Apache service is not reachable on port `8088` (the designated Apache port). The service itself may be running, but it is not accessible.  
You are required to identify and fix the issue using tools like `telnet`, `netstat`, etc.  
**Note:** Make sure that Apache is reachable from the jump host without compromising any security settings.

---

## Tasks

1. **Identify why Apache is not reachable on port 8088.**
2. **Fix the configuration so that Apache is properly accessible on port 8088 from the jump host.**
3. **Test connectivity from the jump host using:**
   ```bash
   curl http://stapp01:8088
   ```

---

## Solution

### 1. SSH into App Server 1

```bash
ssh tony@172.16.238.10
```

---

### 2. Diagnose Listening Services on Port 8088

```bash
netstat -tulpn | grep -i 8088
```

**Sample Output:**
```
tcp        0      0 127.0.0.1:8088          0.0.0.0:*               LISTEN      430/sendmail: accept
```

> **Observation:**  
> The output shows that `sendmail` is using port 8088 on `127.0.0.1`, preventing Apache from binding to this port.

---

### 3. Change Sendmail Port

Edit the Sendmail configuration to use its default port (25) instead of 8088, then restart Sendmail:

```bash
# Edit sendmail configuration if needed
sudo vi /etc/mail/sendmail.cf
# Look for the line with 8088 and change it to 25

sudo systemctl restart sendmail
```

---

### 4. Configure Apache to Listen on Port 8088

Edit the Apache config file to ensure it listens on port 8088:

```bash
sudo vi /etc/httpd/conf/httpd.conf
# or sometimes:
# sudo vi /etc/httpd/ports.conf
```

Make sure you have:
```
Listen 0.0.0.0:8088
```
or
```
Listen 8088
```

---

### 5. Restart Apache Service

```bash
sudo systemctl restart httpd
```

---

### 6. Update iptables to Allow Traffic on Port 8088

```bash
sudo iptables -I INPUT -p tcp --dport 8088 -j ACCEPT
```

To make this change persistent, save the iptables rules:

```bash
sudo service iptables save
```

---

### 7. Test Connectivity from Jump Host

From the jump host, run:

```bash
curl http://stapp01:8088
```

---

### 8. Validation

- Apache should now be reachable on port 8088 from the jump host.
- If you see a response from Apache (even the default page), the issue is resolved.

---

**Result:**  
Apache is accessible on port 8088 from the jump host, and the port conflict with Sendmail is resolved.  
