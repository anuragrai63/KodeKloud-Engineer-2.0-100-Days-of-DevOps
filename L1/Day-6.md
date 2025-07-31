# Instructions

The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

a. Install cronie package on all Nautilus app servers and start crond service.

b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.

# Solution

ssh into the App Servers 

sudo yum install -y cronie
sudo systemctl enable crond
sudo systemctl start crond

echo "*/5 * * * * echo hello > /tmp/cron_text" | sudo tee -a /var/spool/cron/root

# Explanation:

sudo: Runs the command with elevated privileges.

yum: Package manager to install package

systemctl: Enable, Disable, Start & Stop services.

<img width="824" height="56" alt="image" src="https://github.com/user-attachments/assets/77c5fe61-0ac4-4194-a498-406b73ac1233" />

Check the result 
