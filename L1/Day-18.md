# Day 18: Hosting WordPress on Stratos Datacenter

## Instructions

xFusionCorp Industries is planning to host a WordPress website on their infrastructure in the Stratos Datacenter. The infrastructure configuration is already completed (e.g., storage server setup). Complete the following tasks:

1. **Install httpd, PHP, and dependencies on all app hosts.**
2. **Configure Apache to serve on port 8087 on all app hosts.**
3. **Install and configure MariaDB server on the DB server.**
4. **Create a database and user:**
    - Database: `kodekloud_db3`
    - User: `kodekloud_gem`
    - Password: `ksH85UJjhb`
    - Ensure the user can perform all operations on the database.
5. **Verify:** You should be able to access the website on the LBR link (App button on the top bar) and see:  
   `App is able to connect to the database using user kodekloud_gem`

---

## Solution

### 1. Install Apache, PHP, and Dependencies (on each App Host)

```sh
sudo yum install -y httpd php php-mysqlnd php-fpm php-cli
```

---

### 2. Configure Apache to Serve on Port 8087

Open the Apache config file:

```sh
sudo vi /etc/httpd/conf/httpd.conf
```

Change the `Listen` directive:

```
Listen 8087
```

Restart Apache:

```sh
sudo systemctl restart httpd
```

---

### 3. Install and Configure MariaDB (on DB Server)

```sh
sudo yum install -y mariadb-server
sudo systemctl enable mariadb
sudo systemctl start mariadb
```

---

### 4. Create Database and User

Login to MariaDB:

```sh
mysql -u root -p
```

Then run:

```sql
CREATE DATABASE kodekloud_db3;
CREATE USER 'kodekloud_gem'@'%' IDENTIFIED BY 'ksH85UJjhb';
GRANT ALL PRIVILEGES ON kodekloud_db3.* TO 'kodekloud_gem'@'%';
FLUSH PRIVILEGES;
EXIT;
```

**Allow remote connections:**  
Edit `/etc/my.cnf.d/server.cnf` and set:

```
[mysqld]
bind-address=0.0.0.0
```

Restart MariaDB:

```sh
sudo systemctl restart mariadb
```

---

### 5. Deploy WordPress and Configure (on App Host)

```sh
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
```

**Edit `index.php` or the WordPress configuration file (`wp-config.php`):**

```php
define('DB_NAME', 'kodekloud_db3');
define('DB_USER', 'kodekloud_gem');
define('DB_PASSWORD', 'ksH85UJjhb');
define('DB_HOST', 'stdb01');  // Replace 'stdb01' with your DB server hostname if different
```

Set permissions:

```sh
sudo chown -R apache:apache /var/www/html
sudo systemctl restart httpd
```

---

### 6. Verification

- Click on the **App** button (top bar) to view the website.
- You should see the message:  
  `App is able to connect to the database using user kodekloud_gem`

---
