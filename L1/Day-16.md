# Day 16: Load Balancer Setup with Nginx

## Scenario

Day by day, traffic is increasing on one of the websites managed by the Nautilus production support team. As a result, the team has observed a degradation in website performance. After discussions about possible solutions, the team has decided to set up load balancing using Nginx.

---

## Tasks

**a.** Install Nginx on the LBR (Load Balancer) server.

**b.** Configure load balancing in the main Nginx configuration file (`/etc/nginx/nginx.conf`) using the `http` context to balance requests across all App Servers.

**c.** Do **not** update the Apache port that is already defined in the Apache configuration on all app servers. Also, ensure the Apache service is up and running on all app servers.

**d.** Once completed, you can access the website using the **StaticApp** button on the top bar.

---

## Solution

### 1. SSH into Load Balancer Server

```bash
ssh loki@stlb01
```

### 2. Install and Enable Nginx

```bash
sudo yum install -y nginx
sudo systemctl enable nginx
```

### 3. Verify Apache on App Servers and Check Port

Check that Apache is running and note the port (e.g., 5004):

```bash
ssh tony@stapp01 'sudo systemctl status httpd'; sudo ss -tulnp | grep httpd
ssh steve@stapp02 'sudo systemctl status httpd'; sudo ss -tulnp | grep httpd
ssh banner@stapp03 'sudo systemctl status httpd'; sudo ss -tulnp | grep httpd
```

### 4. Edit the Main Nginx Configuration File

Edit `/etc/nginx/nginx.conf` (replace the upstream ports if Apache is running on a port other than 5004):

```nginx
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

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

    # Upstream app servers (use correct Apache port)
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
```

### 5. Start Nginx

```bash
sudo systemctl start nginx
```

---

## 6. Validate

- Click on the **StaticApp** button on the top bar to verify the setup.
- Alternatively, use `curl` or a browser to access the load balancer's IP or domain.

---

## 7. Troubleshooting

- Check Nginx status: `sudo systemctl status nginx`
- Check logs:
  - Access log: `/var/log/nginx/access.log`
  - Error log: `/var/log/nginx/error.log`

---

**Result:**  
If everything is configured properly, the website should load via the load balancer, distributing traffic evenly across all app servers.
