# Day 14: Troubleshooting Apache Service on App Hosts

## Scenario

The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc., running on the systems. One of the monitoring tools detected that Apache is not running as expected on one or more app hosts.

Your task is to identify the faulty app host and fix the issue.  
**Note:** There may not be any code hosted yet on these servers, so you don’t need to worry if Apache shows a default page—just ensure the service is up and running on the correct port.

---

## Tasks

1. **Check the status of Apache on all app hosts (`stapp01`, `stapp02`, `stapp03`) on port `6300`.**
2. **Identify the faulty host where Apache is not running as expected.**
3. **Fix the Apache configuration on the faulty host and ensure the service is running on port `6300`.**
4. **Make sure the Apache service is up and running on all app hosts.**

---

## Solution

### 1. Check Apache Status on All App Hosts

```bash
for host in stapp01 stapp02 stapp03; do
  echo "Checking $host..."
  curl -sI http://$host:6300 >/dev/null && echo "$host is OK" || echo "$host is DOWN"
done
```

**Sample Output:**
```
Checking stapp01...
stapp01 is DOWN

Checking stapp02...
stapp02 is OK

Checking stapp03...
stapp03 is OK
```

---

### 2. Fix Apache Configuration on the Faulty Host (`stapp01` in this example)

#### a. SSH into the faulty host

```bash
ssh tony@stapp01
```

#### b. Edit the Apache configuration file to ensure it listens on port `6300`

```bash
sudo sed -i 's/^Listen .*/Listen 6300/' /etc/httpd/conf/httpd.conf
```

#### c. Verify Apache is listening on the correct port

```bash
sudo ss -ltnp | grep :6300
```

#### d. Update Sendmail port if necessary

Edit `/etc/mail/sendmail.cf` and change the port number if needed, then restart the Sendmail service:

```bash
sudo systemctl restart sendmail
```

#### e. Restart Apache and check status

```bash
sudo systemctl restart httpd
sudo systemctl status httpd
sudo ss -ltnp | grep :6300
```

---

### 3. Verify Apache is Running

```bash
curl -sI http://stapp01:6300 >/dev/null && echo "stapp01 is OK" || echo "stapp01 is DOWN"
```

---

### 4. Validate

- Repeat the Apache status check on all hosts to confirm all are running as expected.

---

**Result:**  
If all steps are followed, Apache should be up and running on port `6300` on all app hosts.
