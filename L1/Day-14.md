# Instructions

The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in Stratos DC.

Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not have hosted any code yet on these servers, so you don’t need to worry if Apache isn’t serving any pages. Just make sure the service is up and running. Also, make sure Apache is running on port 6300 on all app servers.
# Solution
for host in stapp01 stapp02 stapp03; do

  echo "Checking $host..."
  
  curl -sI http://$host:6300 >/dev/null && echo "$host is OK" || echo "$host is DOWN"
  
done

Checking stapp01...
stapp01 is DOWN
Checking stapp02...
stapp02 is OK
Checking stapp03...
stapp03 is OK

# Edit the Apache config file & Sendmail:

sudo sed -i 's/^Listen .*/Listen 6300/' /etc/httpd/conf/httpd.conf

ss -ltnp | grep :6300

Change the port number of Sendmail-- By editing sendmail.cf and restart sendmail service. 

# Restart the HTTPD service and check status-

sudo systemctl restart httpd

sudo systemctl status httpd

sudo ss -ltnp | grep :6300

curl -sI http://stapp01:6300 >/dev/null && echo "$host is OK" || echo "stapp01 is DOWN"

Check the result 
