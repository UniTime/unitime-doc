---
layout: manual
title: Setting up HTTPS for UniTime
---

### Table of Contents
{:.no_toc}
* table
{:toc}
# Setting up HTTPS for UniTime

Based on the instructions from the following websites:

* [https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-18-04)

* [https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-18-04)

* [https://confluence.atlassian.com/adminjiraserver/configuring-apache-reverse-proxy-using-the-ajp-protocol-938847753.html](https://confluence.atlassian.com/adminjiraserver/configuring-apache-reverse-proxy-using-the-ajp-protocol-938847753.html)

### 1. Enable AJP connector on Tomcat

Edit `/etc/tomcat8/server.xml` (e.g., using `sudo vi /etc/tomcat8/server.xml`) and uncomment the following line
```
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
```

To disable access using [http://unitime.university.edu:8080/UniTime](http://unitime.university.edu:8080/UniTime), the following line needs to be commented out in `/etc/tomcat8/server.xml`.
```
<Connector port="8080" protocol="HTTP/1.1"
        connectionTimeout="20000"
        redirectPort="8443" />
```

Restart Tomcat
```
sudo /etc/init.d/tomcat8 restart
```

To change the URL to avoid `/UniTime`, the `UniTime.war` needs to be renamed to `ROOT.war`
```
cd /var/lib/tomcat8/webapps
sudo rm -rf ROOT
sudo mv UniTime.war ROOT.war
```

When this is done while Tomcat is running, this should also undeploy and remove `/var/lib/tomcat8/webapps/UniTime` and replace it with `/var/lib/tomcat8/webapps/ROOT` (containing the unzipped content of the `UniTime WAR` file). If done when tomcat is not running, also remove `/var/lib/tomcat8/webapps/UniTime` folder (`/var/lib/tomcat8/webapps/ROOT` will get created during the first deployment of `ROOT.war`).

### 2. Install Apache2
```
sudo apt install apache2
```

Add AJP Proxy mod
```
sudo a2enmod proxy_ajp
sudo systemctl restart apache2
```

Contigure HTTP access [http://unitime.university.edu](http://unitime.university.edu)

Create `/etc/apache2/sites-available/unitime.conf` file with the following content
```
<VirtualHost *:80>
    ServerName unitime.university.edu
    ProxyPass / ajp://localhost:8009/
    ProxyPassReverse / ajp://localhost:8009/
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Enable `unitime.conf` instead of the `default 000-default.conf`
```
sudo a2ensite unitime.conf
sudo a2dissite 000-default.conf
sudo systemctl reload apache2
```

Verify UniTime works by accessing [http://unitime.university.edu](http://unitime.university.edu).

### 3. Install Cerbot (to request/update Let’s Encrypt certificate)
```
sudo apt install python-certbot-apache
```

Setup certificate
```
sudo certbot --apache -d unitime.university.edu
```

I have used the following options:
```
Enter email address (used for urgent renewal and security notices): administrator@university.edu
Agree on the terms, No on sharing the email with EEF.
Please choose whether or not to redirect HTTP traffic to HTTPS: selected Redirect (option 2)
```

Verify auto-renewal
```
sudo systemctl status certbot.timer
```

Verify that UniTime is running and can be accessed using [https://unitime.university.edu](https://unitime.university.edu)

**Note:** Please note that this creates a new configuration `unitime-le-ssl.conf` with the following content (under `/etc/apache2/sites-available`, no edit is needed)
```
<VirtualHost *:443>
    ServerName unitime.university.edu
    ProxyPass / ajp://localhost:8009/
    ProxyPassReverse / ajp://localhost:8009/
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    SSLCertificateFile /etc/letsencrypt/live/unitime.university.edu/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/unitime.university.edu/privkey.pem
    SSLEngine On
</VirtualHost>
```

And the `unitime.conf` was updated with the following rules added (redirecting HTTP access to HTTPS):
```
RewriteEngine on
RewriteCond %{SERVER_NAME} =unitime.university.edu
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
```