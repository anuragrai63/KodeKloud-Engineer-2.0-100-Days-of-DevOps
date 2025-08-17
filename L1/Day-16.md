Step-by-Step Setup on App Server 2
✅ 1. SSH into App Server 2
bash
ssh steve@stapp02
✅ 2. Install and Enable Nginx
bash
sudo yum install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
✅ 3. Move SSL Certificate and Key to Secure Location
bash
sudo mkdir -p /etc/nginx/ssl
sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/
✅ 4. Configure Nginx for SSL
Edit the default server block:

bash
sudo vi /etc/nginx/nginx.conf
Inside the http block, add this server block (or modify existing one):

nginx
server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    location / {
        root   /usr/share/nginx/html;
        index  index.html;
    }
}
Save and exit.

✅ 5. Create index.html with Welcome Message
bash
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
✅ 6. Restart Nginx to Apply Changes
bash
sudo systemctl restart nginx
✅ 7. Test from Jump Host
From the jump host, run:

bash
curl -Ik https://stapp02
Or use IP if DNS isn’t configured:

bash
curl -Ik https://<stapp02-IP>
Expected output:

Code
HTTP/1.1 200 OK
...
