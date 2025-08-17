# Instructions
The system admins team of xFusionCorp Industries needs to deploy a new application on App Server 2 in Stratos Datacenter. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:

1. Install and configure nginx on App Server 2.

2. On App Server 2 there is a self signed SSL certificate and key present at location /tmp/nautilus.crt and /tmp/nautilus.key. Move them to some appropriate location and deploy the same in Nginx.

3. Create an index.html file with content Welcome! under Nginx document root.

4. For final testing try to access the App Server 2 link (either hostname or IP) from jump host using curl command. For example curl -Ik https://<app-server-ip>/.

# Solution
ssh steve@stapp02

sudo yum install -y nginx;sudo systemctl enable nginx;sudo systemctl start nginx

# Move SSL Certificate and Key to Secure Location

sudo mkdir -p /etc/nginx/ssl

sudo mv /tmp/nautilus.crt /etc/nginx/ssl/

sudo mv /tmp/nautilus.key /etc/nginx/ssl/

# Configure Nginx for SSL
sudo vi /etc/nginx/nginx.conf

Inside the http block, add this server block (or modify existing one):


''server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    location / {
        root   /usr/share/nginx/html;
        index  index.html;
    }
}''

# Create index.html with Welcome Message
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html

# Restart Nginx to Apply Changes & Test from Jump Host
sudo systemctl restart nginx

curl -Ik https://stapp02

Check the result 
