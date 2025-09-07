# Instructions
xFusionCorp Industries is planning to host a WordPress website on their infra in Stratos Datacenter. They have already done infrastructure configuration—for example, on the storage server they already have a shared directory /vaw/www/html that is mounted on each app host under /var/www/html directory. Please perform the following steps to accomplish the task:

a. Install httpd, php and its dependencies on all app hosts.

b. Apache should serve on port 8087 within the apps.

c. Install/Configure MariaDB server on DB Server.

d. Create a database named kodekloud_db3 and create a database user named kodekloud_gem identified as password ksH85UJjhb. Further make sure this newly created user is able to perform all operation on the database you created.

e. Finally you should be able to access the website on LBR link, by clicking on the App button on the top bar. You should see a message like App is able to connect to the database using user kodekloud_gem

# Solution
ssh each app hosts:

sudo yum install -y httpd php php-mysqlnd php-fpm php-cli

Configure Apache to Serve on Port 8087

sudo vi /etc/httpd/conf/httpd.conf

Change the Listen directive:

Listen 8087

Restart:-

sudo systemctl restart httpd

# Install and Configure MariaDB on DB Server
sudo yum install -y mariadb-server

sudo systemctl enable mariadb

sudo systemctl start mariadb

# Create Database and User
mysql -u root -p

CREATE DATABASE kodekloud_db3;
CREATE USER 'kodekloud_gem'@'%' IDENTIFIED BY 'ksH85UJjhb';
GRANT ALL PRIVILEGES ON kodekloud_db3.* TO 'kodekloud_gem'@'%';
FLUSH PRIVILEGES;
EXIT;

# Ensure MariaDB allows remote connections: /etc/my.cnf.d/server.cnf
[mysqld]
bind-address=0.0.0.0

# Restart DB
sudo systemctl restart mariadb

# Deploy WordPress and Verify on App Host:-

cd /var/www/html

sudo wget https://wordpress.org/latest.tar.gz

sudo tar -xzf latest.tar.gz

sudo mv wordpress/* .

sudo rm -rf wordpress latest.tar.gz

# Edit index.php

define('DB_NAME', 'kodekloud_db3');
define('DB_USER', 'kodekloud_gem');
define('DB_PASSWORD', 'ksH85UJjhb');
define('DB_HOST', 'stdb01');

sudo chown -R apache:apache /var/www/html

sudo systemctl restart httpd

# Click on App to view status 

Check the result 
