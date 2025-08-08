# Instructions

Tur monitoring tool has reported an issue in Stratos Datacenter. One of our app servers has an issue, as its Apache service is not reachable on port 8088 (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.

Use tools like telnet, netstat, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

Once fixed, you can test the same using command curl http://stapp01:8088 command from jump host.

# Solution

ssh into the App Server 1: `ssh tony@172.16.238.10`

netstat -tulpn |grep -i 8088

tcp        0      0 127.0.0.1:8088          0.0.0.0:*               LISTEN      430/sendmail: accept

Change Port number of Sendmail from 8088 to 25

Verify the portnumber of apache

sudo vi /etc/httpd/conf/httpd.conf   # or ports.conf

Restart the Apache server

systemctl restart httpd

update the IPTables

sudo iptables -I INPUT -p tcp --dport 8088 -j ACCEPT

curl http://stapp01:8088

# Explanation:

Check that Apache is running and configured to listen on port 8082, updating the config if needed. Ensure the firewall allows traffic on port 8082, then verify access from the jump host using curl

Check the result 
