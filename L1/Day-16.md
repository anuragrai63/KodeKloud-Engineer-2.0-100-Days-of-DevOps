# Instructions
Day by day traffic is increasing on one of the websites managed by the Nautilus production support team. Therefore, the team has observed a degradation in website performance. Following discussions about this issue, the team has decided to deploy this application on a high availability stack i.e on Nautilus infra in Stratos DC. They started the migration last month and it is almost done, as only the LBR server configuration is pending. Configure LBR server as per the information given below:

a. Install nginx on LBR (load balancer) server.

b. Configure load-balancing with the an http context making use of all App Servers. Ensure that you update only the main Nginx configuration file located at /etc/nginx/nginx.conf.

c. Make sure you do not update the apache port that is already defined in the apache configuration on all app servers, also make sure apache service is up and running on all app servers.

d. Once done, you can access the website using StaticApp button on the top bar.

# Solution

ssh loki@stlb01

sudo yum install -y nginx

sudo systemctl enable nginx

Verify Apache on App Servers With port number 

ssh tony@stapp01 'sudo systemctl status httpd';sudo ss -tulnp | grep httpd

ssh steve@stapp02 'sudo systemctl status httpd';sudo ss -tulnp | grep httpd

ssh banner@stapp03 'sudo systemctl status httpd';sudo ss -tulnp | grep httpd

# Edit the main Nginx config file:

"
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 4096;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Upstream app servers (use correct Apache port, e.g. 8080)
    upstream backend {
        server stapp01:5004;
        server stapp02:5004;
        server stapp03:5004;
    }

    # Load balancer server block
    server {
        listen 80;
        server_name _;

        location / {
            proxy_pass http://backend;
            proxy_http_version 1.1;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
"

sudo systemctl start nginx

Click on static app to see status--

Check the result 
