# Instructions

The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:

Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

# Solution

Log in to the database server using SSH:

ssh peter@172.16.239.10

Check DB status 

sudo systemctl status mariadb

Start DB

sudo systemctl start mariadb

It will throw below error

Job for mariadb.service failed because the control process exited with error code.
See "systemctl status mariadb.service" and "journalctl -xeu mariadb.service" for details.

Check log

sudo cat /var/log/mariadb/mariadb.log

Check Permission

ls -ld /run/mariadb

Correct Permission

sudo chown -R mysql:mysql /run/mariadb

Restart Service

sudo systemctl restart mariadb

# Explanation:

The directory /run/mariadb/ must be owned by the mysql user and writable.

<img width="1718" height="450" alt="image" src="https://github.com/user-attachments/assets/0dc37ad7-461d-492f-9398-c7e974295357" />


Check the result 
