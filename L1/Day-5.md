# Day 5: Disabling SELinux for Initial Testing

## Scenario

Following a security audit, the xFusionCorp Industries security team has decided to enhance application and server security using SELinux. For initial testing, the following requirements must be met:

---

## Tasks

- **Install the required SELinux packages.**
- **Permanently disable SELinux for now** (it will be re-enabled after future configuration changes).
- **No reboot needed** at this time; a scheduled reboot will occur later.
- **Disregard current SELinux status** via the command line; the final status after reboot should be disabled.

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@172.16.238.11
```

---

### 2. Install SELinux Packages

```bash
sudo yum install -y selinux-policy selinux-policy-targeted
```

---

### 3. Permanently Disable SELinux

Modify the SELinux configuration file to set SELINUX to `disabled`:

```bash
sudo sed -i 's/^SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```

---

## Explanation

- **sudo:** Runs the command as a superuser or with elevated privileges.
- **yum:** Installs the necessary SELinux policy packages.
- **sed:** Edits the `/etc/selinux/config` file in place.
    - `s/^SELINUX=enforcing/SELINUX=disabled/` replaces the line that starts with `SELINUX=enforcing` to `SELINUX=disabled`.
- No need to reboot now; changes will take effect after the next system reboot.

---

**Result:**  
SELinux is set to be disabled after the next reboot, as required for initial testing.
