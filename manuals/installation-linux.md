---
layout: manual
title: Setting up UniTime on Linux server
version: 4.1
---

1. Install MySQL
```
sudo apt-get install mysql-server
```

2. Install Oracle Java 8
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

3. Install Tomcat 8
```
sudo apt-get install tomcat8
sudo /etc/init.d/tomcat8 stop
```

    In `/etc/default/tomcat8`, increase the Xmx parameter:
    ```
    JAVA_OPTS="-Djava.awt.headless=true -Xmx2g -XX:+UseConcMarkSweepGC"
    ```

4. Install MySQL JDBC driver
```
wget https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.38/mysql-connector-java-5.1.38.jar
sudo cp mysql-connector-java-5.1.38.jar /var/lib/tomcat8/lib/
```

    Alternatively, the driver can be downloaded from [mvnrepository.com](https://mvnrepository.com/artifact/mysql/mysql-connector-java) or [dev.mysql.com/downloads](https://dev.mysql.com/downloads/connector/j/). Please make sure you use the driver version matching your MySQL database (as installed in step 1).


5. Install UniTime

    Download and unzip UniTime
    ```
    wget https://github.com/UniTime/unitime/releases/download/v4.1.175/unitime-4.1_bld175.zip
    unzip unitime-4.1_bld175.zip -d unitime
    ```

    Create timetable database
    ```
    mysql -uroot -p -f <unitime/doc/mysql/schema.sql
    mysql -utimetable -punitime <unitime/doc/mysql/woebegon-data.sql
    ```

    Create folder `/var/lib/tomcat8/data`
    ```
    sudo mkdir /var/lib/tomcat8/data
    sudo chown tomcat8 /var/lib/tomcat8/data
    ```

    Deploy `UniTime.war`
    ```
    sudo cp unitime/web/UniTime.war /var/lib/tomcat8/webapps
    ```


6. UniTime custom properties ***(optional step)***

    In `/etc/tomcat8/catalina.properties` add:
    ```
    tmtbl.custom.properties=/etc/tomcat8/unitime.properties
    ```

    Create file /etc/tomcat8/unitime.properties (leave it empty for now, unitime custom properties go there)
    ```
    touch /etc/tomcat8/unitime.properties
    sudo chown tomcat8 /etc/tomcat8/unitime.properties
    ```

7. Allow Tomcat8 to run on port 80 instead of the default 8080 ***(optional step)***
```
sudo apt-get install authbind
sudo touch /etc/authbind/byport/80
sudo chmod 500 /etc/authbind/byport/80
sudo chown tomcat8 /etc/authbind/byport/80
```

    In /etc/default/tomcat8 set
    ```
    AUTHBIND=yes
    ```

    In `/etc/tomcat8/server.xml`, change the non-SSL/TLS HTTP/1.1 connector port to 80 (was 8080)
    ```
    <Connector port="80" protocol="HTTP/1.1" ... />
    ```

8. Start Tomcat
```
sudo /etc/init.d/tomcat8 start
```


9. Check the logs for any errors ***(optional step)***
```
tail -n 1000 -f /var/log/tomcat8/catalina.out
```


UniTime should be available at [http://localhost/UniTime](http://localhost/UniTime) (or [http://localhost:8080/UniTime](q=http://localhost:8080/UniTime) when step 7 was skipped).



