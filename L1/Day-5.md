# Instructions

Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 2 in the Stratos Datacenter:

Install the required SELinux packages.

Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.

No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.

Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

# Solution

ssh into the App Server 2: `ssh steve@172.16.238.11`

sudo yum install -y selinux-policy selinux-policy-targeted

sudo sed -i 's/^SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config


# Explanation:

sudo: Runs the command with elevated privileges.

sed: Stream editor for filtering and transforming text.

-i: Edits the file in place.

's/^SELINUX=enforcing/SELINUX=disabled/': Substitutes the line starting with SELINUX=enforcing with SELINUX=disabled.

<img width="1270" height="198" alt="image" src="https://github.com/user-attachments/assets/6536a7cc-0cf3-433e-b793-c348d4846ef2" />

Check the result 
