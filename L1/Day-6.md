# Day 6: Setting Up Scheduled Automation with Cron

## Scenario

The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want these scripts to be deployed on all app servers in Stratos DC and executed on a set schedule.  
Before deploying, they need to verify cron functionality on all app servers.

---

## Tasks

a. **Install the `cronie` package** on all Nautilus app servers and start the `crond` service.  
b. **Add a cron job** for the `root` user to run every 5 minutes:
   ```
   */5 * * * * echo hello > /tmp/cron_text
   ```

---

## Solution

### 1. SSH into Each App Server

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

---

### 2. Install Cronie and Start crond Service

```bash
sudo yum install -y cronie
sudo systemctl enable crond
sudo systemctl start crond
```

---

### 3. Add the Cron Job for Root User

```bash
echo "*/5 * * * * echo hello > /tmp/cron_text" | sudo tee -a /var/spool/cron/root
```

---

## Explanation

- **sudo**: Runs commands with elevated privileges.
- **yum**: Installs the `cronie` package, which provides cron on CentOS/RedHat systems.
- **systemctl**: Used to enable and start the `crond` service.
- The cron job writes "hello" to `/tmp/cron_text` every 5 minutes as the root user.

---

**Result:**  
A cron job is now set up and will execute every 5 minutes on each app server, confirming that scheduled automation is working as intended.
