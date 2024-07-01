---
layout: manual
title: Setting up UniTime on Linux server
version: 4.8
---

1. Install MySQL 8.0

    ```
    sudo apt install mysql-server
    ```

    If the above command does not work, you may need to add MySQL Software repository first. See [How To Install the Latest MySQL on Debian 10
](https://www.digitalocean.com/community/tutorials/how-to-install-the-latest-mysql-on-debian-10) for more details.
    ```
    sudo apt update
    sudo apt install gnupg
    wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
    sudo dpkg -i mysql-apt-config_0.8.22-1_all.deb
    sudo apt update
    sudo apt install mysql-server
    ```

2. Install Java 11 or later
```
sudo apt install openjdk-11-jdk
```

3. Install Tomcat 9
```
sudo apt install tomcat9
sudo systemctl stop tomcat9
```

    In `/etc/default/tomcat9`, increase the Xmx parameter:
    ```
    JAVA_OPTS="-Djava.awt.headless=true -Xmx2g"
    ```

4. Install MySQL JDBC driver
```
wget https://repo1.maven.org/maven2/com/mysql/mysql-connector-j/8.0.33/mysql-connector-j-8.0.33.jar
sudo cp mysql-connector-j-8.0.33.jar /var/lib/tomcat9/lib/
```

    Alternatively, the driver can be downloaded from [mvnrepository.com](https://mvnrepository.com/artifact/com.mysql/mysql-connector-j) or [dev.mysql.com/downloads](https://dev.mysql.com/downloads/connector/j/). Please make sure you use the driver version matching your MySQL database (as installed in step 1).


5. Install UniTime

    Download and unzip UniTime
    ```
    wget https://github.com/UniTime/unitime/releases/download/v4.8.139/unitime-4.8_bld139.zip
    unzip unitime-4.8_bld139.zip -d unitime
    ```

    Create timetable database
    ```
    mysql -uroot -p -f <unitime/doc/mysql/schema.sql
    mysql -utimetable -punitime <unitime/doc/mysql/woebegon-data.sql
    ```

    Create folder `/var/lib/tomcat9/data`
    ```
    sudo mkdir /var/lib/tomcat9/data
    sudo chown tomcat9 /var/lib/tomcat9/data
    ```

    Deploy `UniTime.war`
    ```
    sudo cp unitime/web/UniTime.war /var/lib/tomcat9/webapps
    ```


6. UniTime custom properties ***(optional step)***

    In `/etc/tomcat9/catalina.properties` add:
    ```
    tmtbl.custom.properties=/etc/tomcat9/unitime.properties
    ```

    Create file /etc/tomcat9/unitime.properties (leave it empty for now, unitime custom properties go there)
    ```
    touch /etc/tomcat9/unitime.properties
    sudo chown tomcat9 /etc/tomcat9/unitime.properties
    ```

7. Allow Tomcat to run on port 80 instead of the default 8080 ***(optional step)***
    ```
    sudo apt install authbind
    sudo touch /etc/authbind/byport/80
    sudo chmod 500 /etc/authbind/byport/80
    sudo chown tomcat9 /etc/authbind/byport/80
    ```

    In /etc/default/tomcat9 set
    ```
    AUTHBIND=yes
    ```

    In `/etc/tomcat9/server.xml`, change the non-SSL/TLS HTTP/1.1 connector port to 80 (was 8080)
    ```
    <Connector port="80" protocol="HTTP/1.1" ... />
    ```

8. Start Tomcat
    ```
    sudo systemctl start tomcat9
    ```


9. Check the logs for any errors ***(optional step)***
    ```
    tail -n 1000 -f /var/log/tomcat9/catalina.out
    ```


    UniTime should be available at [http://localhost/UniTime](http://localhost/UniTime) (or [http://localhost:8080/UniTime](q=http://localhost:8080/UniTime) when step 7 was skipped).



