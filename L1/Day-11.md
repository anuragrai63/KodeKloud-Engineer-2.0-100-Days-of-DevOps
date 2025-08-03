# Instructions

The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. After an internal team meeting, they have decided to use the tomcat application server. Based on the requirements mentioned below complete the task:

a. Install tomcat server on App Server 1.

b. Configure it to run on port 3001.

c. There is a ROOT.war file on Jump host at location /tmp.

Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e curl http://stapp01:3001

# Solution

ssh into the App Server 1: `ssh tony@172.16.238.10`

sudo yum install -y tomcat

sudo vi /etc/tomcat/server.xml

<Connector port="3001" protocol="HTTP/1.1"

sudo systemctl restart tomcat

scp /tmp/ROOT.war tony@172.16.238.10:/tmp/

sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/

# Explanation:

During the above process we have installed the tomcat and updated asked ports in config.

<img width="1830" height="776" alt="image" src="https://github.com/user-attachments/assets/fd54f5db-61ab-4c67-9191-f026902db672" />

Check the result 
