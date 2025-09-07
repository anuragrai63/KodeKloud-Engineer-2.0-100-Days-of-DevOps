# Day 11: Deploying a Java Application with Tomcat

## Scenario

The Nautilus application development team has completed the beta version of a Java-based application. They plan to deploy it on **App Server 1** in Stratos DC. After a successful deployment, the application should be accessible using the base URL.

---

## Tasks

a. **Install Tomcat server on App Server 1.**  
b. **Configure Tomcat to run on port 3001.**  
c. **Deploy the provided `ROOT.war` file (located at `/tmp` on the Jump Host) to the Tomcat server.**  
d. **Ensure the web page is accessible at the base URL:**  
   ```bash
   curl http://stapp01:3001
   ```

---

## Solution

### 1. SSH into App Server 1

```bash
ssh tony@172.16.238.10
```

---

### 2. Install Tomcat

```bash
sudo yum install -y tomcat
```

---

### 3. Configure Tomcat to Listen on Port 3001

Edit the Tomcat server configuration:

```bash
sudo vi /etc/tomcat/server.xml
```

Locate the following section and update the port to `3001`:
```xml
<Connector port="3001" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```

---

### 4. Restart Tomcat for Changes to Take Effect

```bash
sudo systemctl restart tomcat
```

---

### 5. Deploy the `ROOT.war` File

From the **Jump Host**, copy the `ROOT.war` file to App Server 1:

```bash
scp /tmp/ROOT.war tony@172.16.238.10:/tmp/
```

On **App Server 1**, move `ROOT.war` to the Tomcat webapps directory:

```bash
sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/
```

---

### 6. Validate the Deployment

Run the following command from the Jump Host or any system with access to App Server 1:

```bash
curl http://stapp01:3001
```

You should see the application’s web page as a response.

---

## Explanation

- Tomcat was installed and configured to listen on the required port.
- The provided `ROOT.war` was deployed to the Tomcat server, making the application accessible at the base URL.
- This approach ensures the application is served directly at `http://stapp01:3001` without needing any additional context path.

---

**Result:**  
If everything is set up correctly, accessing `http://stapp01:3001` should display the deployed Java application.
