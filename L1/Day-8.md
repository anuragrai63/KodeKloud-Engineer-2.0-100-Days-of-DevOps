# Day 8: Installing Ansible with pip3

## Scenario

During the weekly meeting, the Nautilus DevOps team discussed automation and configuration management solutions to implement. After considering several options, the team decided to use Ansible and set it up on the Jump Host.

---

## Task

**Install Ansible version 4.10.0 on the Jump Host using pip3 only. Ensure the Ansible binary is available globally so all users on this system can run Ansible commands.**

---

## Solution

### 1. Install `python3-pip` (if not already installed)

```bash
sudo yum install python3-pip -y
```

---

### 2. Install Ansible version 4.10.0 globally using pip3

```bash
sudo pip3 install ansible==4.10.0
```

---

### 3. Verify Ansible Installation

```bash
ansible --version
```

---

## Explanation

- **yum:** The default package manager for installing system packages (here, to install pip3).
- **pip3:** Python package manager used to install Python modules and packages (here, to install Ansible).
- The use of `sudo` ensures Ansible is installed globally and accessible to all users.

---

**Result:**  
Ansible 4.10.0 is now installed globally on the Jump Host and can be accessed by any user by running `ansible` commands from the terminal.
