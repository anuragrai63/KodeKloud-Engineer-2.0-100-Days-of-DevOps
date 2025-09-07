# Day 9: Setting Up Password-less SSH Authentication for Automation

## Scenario

The system admins team of xFusionCorp Industries has created scripts on the jump host that routinely perform operations on all app servers in the Stratos Datacenter. To ensure these scripts run smoothly and non-interactively, password-less SSH authentication needs to be set up from the user `thor` on the jump host to all app servers, using their respective sudo users.

---

## Task

**Set up password-less authentication from user `thor` on the jump host to all app servers through their respective sudo users.**

---

## Solution

### 1. Log in to the Jump Host as `thor`

```bash
ssh thor@jump_host_ip
```

---

### 2. Generate an SSH Key Pair (if not already present)

```bash
ssh-keygen -t rsa
```
- Accept the default file location and leave the passphrase empty for automation.

---

### 3. Copy the Public Key to Each App Server

Replace `<user>` and `<app_server_ip>` with the respective sudo user and app server IP:

```bash
ssh-copy-id <user>@<app_server_ip>
```

For example, if the sudo users are `tony`, `steve`, and `banner` for `stapp01`, `stapp02`, and `stapp03` respectively:

```bash
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
```

---

### 4. Test Password-less SSH Login

Ensure you can connect without being prompted for a password:

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

---

## Explanation

- **SSH key pair** allows secure, password-less logins, which is ideal for automation.
- **`ssh-copy-id`** simplifies copying the public key to the target server’s `~/.ssh/authorized_keys` file.
- This setup ensures that automation scripts from the jump host can run commands on all app servers without manual password entry.

---

**Result:**  
Password-less SSH authentication is now configured from `thor` on the jump host to all app servers via their respective sudo users. This enables seamless, non-interactive script execution across the infrastructure.
