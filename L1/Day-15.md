# Day 15: Nginx SSL Setup on App Server 2

## Scenario

The system admins team of xFusionCorp Industries needs to deploy a new application on **App Server 2** in the Stratos Datacenter. There are some prerequisites to prepare the server for application deployment, which include installing and configuring Nginx with SSL.

---

## Tasks

1. **Install and configure Nginx on App Server 2.**
2. **Move the self-signed SSL certificate and key** (located at `/tmp/nautilus.crt` and `/tmp/nautilus.key`) to an appropriate location and configure them in Nginx.
3. **Create an `index.html` file** with content `Welcome!` under the Nginx document root.
4. **Test access:** From the jump host, access App Server 2 using the `curl` command:
   ```bash
   curl -Ik https://<app-server-ip>/
   ```

---

## Solution

### 1. SSH into App Server 2

```bash
ssh steve@stapp02
```

---

### 2. Install and Enable Nginx

```bash
sudo yum install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

---

### 3. Move SSL Certificate and Key to Secure Location

```bash
sudo mkdir -p /etc/nginx/ssl
sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/
```

---

### 4. Configure Nginx for SSL

Edit the Nginx configuration file:

```bash
sudo vi /etc/nginx/nginx.conf
```

Inside the `http` block, add (or modify) the following `server` block:

```nginx
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
```

---

### 5. Create `index.html` with Welcome Message

```bash
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
```

---

### 6. Restart Nginx to Apply Changes

```bash
sudo systemctl restart nginx
```

---

### 7. Test from Jump Host

From the jump host, run:

```bash
curl -Ik https://stapp02
```

---

### 8. Validate

- Ensure you receive a valid HTTP response over HTTPS.
- The output should show the server response headers and a status code (e.g., 200 OK).

---

**Result:**  
If everything is configured correctly, you should be able to access App Server 2 via HTTPS and see the `Welcome!` message.
