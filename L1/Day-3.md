# Instructions

Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.

Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.


# Solution

ssh into the App Server 1: `ssh tony@172.16.238.10`

ssh into the App Server 2: `ssh steve@172.16.238.11`

ssh into the App Server 3: `ssh banner@172.16.238.12`

sudo sed -i 's/^PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config && sudo systemctl restart sshd


# Explanation:

sudo: Runs the command with administrative privileges.

sed -i 's/^PermitRootLogin.*/PermitRootLogin no/': search and replace parameter


<img width="1426" height="260" alt="image" src="https://github.com/user-attachments/assets/7f82cc4d-78c2-4de8-9f5f-881ea5e2092c" />


Check the result 
