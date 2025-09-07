# Instructions
The Nautilus application development team is planning to launch a new PHP-based application, which they want to deploy on Nautilus infra in Stratos DC. The development team had a meeting with the production support team and they have shared some requirements regarding the infrastructure. Below are the requirements they shared:

a. Install nginx on app server 3 , configure it to use port 8098 and its document root should be /var/www/html.

b. Install php-fpm version 8.3 on app server 3, it must use the unix socket /var/run/php-fpm/default.sock (create the parent directories if don't exist).

c. Configure php-fpm and nginx to work together.

d. Once configured correctly, you can test the website using curl http://stapp03:8098/index.php command from jump host.

NOTE: We have copied two files, index.php and info.php, under /var/www/html as part of the PHP-based application setup. Please do not modify these files.

# Solution
ssh app3 hosts:

sudo yum install nginx -y

Edit the default server block:

sudo vi /etc/nginx/conf.d/default.conf

Replace its contents with:

server {
    listen 8098;
    server_name stapp03;

    root /var/www/html;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/var/run/php-fpm/default.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}

Install PHP-FPM 8.3:- 

sudo dnf -y install epel-release

sudo dnf -y install https://rpms.remirepo.net/enterprise/remi-release-9.rpm

Reset PHP module and enable the 8.3 stream:

sudo dnf -y module reset php

sudo dnf -y module enable php:remi-8.3

Install PHP-FPM 8.3 and common extensions:

sudo dnf -y install php-fpm php-cli php-common php-opcache php-mbstring php-xml php-gd php-intl php-mysqlnd php-zip

Verify:

php -v (should show PHP 8.3.x)

Configure PHP-FPM to Use Custom Socket:

sudo mkdir -p /var/run/php-fpm

Edit the PHP-FPM pool config:

sudo vi /etc/php-fpm.d/www.conf

Update these lines:

listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660

Start and Enable Services:

sudo systemctl enable php-fpm nginx

sudo systemctl start php-fpm nginx

# Test the Setup
From the jump host, run:

curl http://stapp03:8098/index.php

Check the result 
