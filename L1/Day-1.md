# Day 1: Creating a User with a Non-Interactive Shell

## Scenario

To meet the requirements of the backup agent tool, the system admin team at xFusionCorp Industries needs to create a user account that cannot log in interactively.

---

## Task

**Create a user named `john` with a non-interactive shell on App Server 3.**

---

## Solution

### 1. SSH into App Server 3

```bash
ssh banner@172.16.238.12
```

---

### 2. Create the User with a Non-Interactive Shell

```bash
sudo useradd -m -s /sbin/nologin john
```

---

## Explanation

- **sudo**: Runs the command with administrative privileges.
- **useradd**: Command to create a new user.
- **-m**: Creates a home directory for the user.
- **-s /sbin/nologin**: Assigns `/sbin/nologin` as the user's shell, preventing interactive login.

---

**Result:**  
A user named `john` is created with a non-interactive shell, ensuring the account cannot be used for standard logins but is available for automated processes.
