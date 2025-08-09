# Instructions

We have one of our websites up and running on our Nautilus infrastructure in Stratos DC. Our security team has raised a concern that right now Apache’s port i.e 5004 is open for all since there is no firewall installed on these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:

1. Install iptables and all its dependencies on each app host.

2. Block incoming port 5004 on all apps for everyone except for LBR host.

3. Make sure the rules remain, even after system reboot.

# Solution

ssh into the App Servers 

grep -Ei 'lb|lbr' /etc/hosts

# Example output:

# 172.16.238.14  stlb01

sudo yum install -y iptables iptables-services

# Avoid conflicts with firewalld (if present)

sudo systemctl stop firewalld 2>/dev/null || true

sudo systemctl disable firewalld 2>/dev/null || true

# Enable iptables service

sudo systemctl enable --now iptables

LBR_IP=172.16.238.14   

# Start clean for INPUT chain

sudo iptables -F INPUT

# Baseline safe allows

sudo iptables -A INPUT -i lo -j ACCEPT

sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Allow SSH (optional but recommended if you connect via 22)

sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow Apache 5004 ONLY from LBR

sudo iptables -A INPUT -p tcp -s "$LBR_IP" --dport 5004 -j ACCEPT

# Drop everyone else on 5004

sudo iptables -A INPUT -p tcp --dport 5004 -j DROP

# Save rules for persistence

sudo service iptables save

sudo systemctl restart iptables

Check the result 
