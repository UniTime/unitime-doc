---
layout: manual
title: Setting up UniTime on Mac
version: 4.8
---

### Table of Contents
{:.no_toc}
* table
{:toc}


# 1. Install Oracle Java 11 or later


Download Java JDK from [https://www.oracle.com/java/technologies/downloads](https://www.oracle.com/java/technologies/downloads/#jdk21-mac) (a file named like `jdk-22_macos-aarch64_bin.dmg`), start it up and follow the installation instructions


![Setting up UniTime on Mac](images/installation-mac-java1.png){:class='screenshot'}


Click Continue


![Setting up UniTime on Mac](images/installation-mac-java2.png){:class='screenshot'}


Click Continue


![Setting up UniTime on Mac](images/installation-mac-java3.png){:class='screenshot'}

Click Install


![Setting up UniTime on Mac](images/installation-mac-java4.png){:class='screenshot'}


Wait for the installation to finish...


![Setting up UniTime on Mac](images/installation-mac-java5.png){:class='screenshot'}


Click Close


# 2. Install MySQL 8.0


Download MySQL Community Server from [https://dev.mysql.com/downloads/mysql](https://dev.mysql.com/downloads/mysql) (a file named like `mysql-8.0.37-macos14-arm64.dmg`), start it up and follow the installation instructions.


![Setting up UniTime on Mac](images/installation-mac-mysql1.png){:class='screenshot'}


Click Continue


![Setting up UniTime on Mac](images/installation-mac-mysql2.png){:class='screenshot'}

Click Continue

![Setting up UniTime on Mac](images/installation-mac-mysql3.png){:class='screenshot'}

Accept the license by clicking Agree


![Setting up UniTime on Mac](images/installation-mac-mysql4.png){:class='screenshot'}

Click Continue

![Setting up UniTime on Mac](images/installation-mac-mysql5.png){:class='screenshot'}

Click Install

![Setting up UniTime on Mac](images/installation-mac-mysql6.png){:class='screenshot'}

Wait for the installation to finish. Select **Use Legact Password Encryption**, click Next

![Setting up UniTime on Mac](images/installation-mac-mysql7.png){:class='screenshot'}

Fill in the "root" password, click Finish.

![Setting up UniTime on Mac](images/installation-mac-mysql8.png){:class='screenshot'}

Click Close

# 3. Install Apache Tomcat 9.0

**Note:** Tomcat 10 or later are currenrtly not supported!

Download Apache Tomcat 9.0 from [https://tomcat.apache.org/download-90.cgi](https://tomcat.apache.org/download-90.cgi) (choose zip option, a file named like `apache-tomcat-9.0.90.zip`), unzip the archive by double clicking on its name.

![Setting up UniTime on Mac](images/installation-mac-tomcat1.png){:class='screenshot'}

The Apache Tomcat does not have any Mac installation. It could be just started up using the startup.sh in the bin folder, but do not do that just yet.

Note: The unzipped `apache-tomcat-9.0.90` is left in the Downloads folder, but it can be moved some place else if needed. This could be done at any time or after the installation is done.

## 3a. Add -Xmx parameter

To ensure that the Tomcat will be able to allocate enough memory, we need to set the -Xm parameter. In this manual it is set to 2 GB, but some other number can be used.


Open `apache-tomcat-9.0.90/bin/catalina.sh` file in a text editor (e.g., right click on the file > Open with … > Other > select TextEdit). Add the following line at the top of the file (as the second line):

```
export JAVA_OPTS="${JAVA_OPTS} -Xmx2g -Djava.awt.headless=true"
```


Save the file. It should look like this (note the second line):


![Setting up UniTime on Mac](images/installation-mac-tomcat2.png){:class='screenshot'}

## 3b. Make tomcat scripts executable


In the terminal (open Launchpad > Other > Terminal), execute the following command


```
chmod +x ~/Downloads/apache-tomcat-9.0.90/bin/*sh
```

![Setting up UniTime on Mac](images/installation-mac-tomcat3.png){:class='screenshot'}



# 4. Install MySQL JDBC driver


Download MySQL Connector/J driver from [https://dev.mysql.com/downloads/connector/j](https://dev.mysql.com/downloads/connector/j) (choose Platform Independent ZIP Archive, a file named like `mysql-connector-j-8.0.33.zip`). Unzip the downloaded file (double click the downloaded file). In `mysql-connector-j-8.0.33`, copy the extracted `mysql-connector-j-8.0.33.jar` into `apache-tomcat-9.0.90/lib`.


![Setting up UniTime on Mac](images/installation-mac-jdbc.png){:class='screenshot'}



# 5. Install UniTime


Download UniTime from [https://github.com/UniTime/unitime/releases/latest](https://github.com/UniTime/unitime/releases/latest) (a file named like `unitime-4.8_bld139.zip`) and unzip it (double click the downloaded file).

## 5a. Create and populate the timetable database


Start the Terminal (Launchpad > Other > Terminal), execute:


```
/usr/local/mysql/bin/mysql -u root -p -f <~/Downloads/unitime-4.8_bld139/doc/mysql/schema.sql
/usr/local/mysql/bin/mysql -utimetable -punitime <~/Downloads/unitime-4.8_bld139/doc/mysql/woebegon-data.sql
```


When prompted, use the MySQL root user password as provided in step 2b. You can safely ignore the DROP USER failed error (the script tries to drop the timetable user first).



![Setting up UniTime on Mac](images/installation-mac-database.png){:class='screenshot'}

## 5b. Deploy the UniTime application


Copy `unitime-4.8_bld139/web/UniTime.war` (from the unzipper UniTime archive) to `apache-tomcat-9.0.90/webapps`


![Setting up UniTime on Mac](images/installation-mac-war.png){:class='screenshot'}

## 5c. Create UniTime custom properties file ***(optional step)***


Create `apache-tomcat-9.0.90/conf/unitime.properties` file (e.g., by using the TextEdit application). Please note that if you are using TextEdit, you need to select Format > Make Plain Text in order to make the file plain text.


![Setting up UniTime on Mac](images/installation-mac-custom1.png){:class='screenshot'}


Open `apache-tomcat-9.0.90/conf/catalina.properties` file in a text editor (e.g., right click on the file > Open with … > Other > select TextEdit). Add the following line at the bottom of the file:

```
tmtbl.custom.properties=/Users/<user>/Downloads/apache-tomcat-9.0.90/conf/unitime.properties
```


The `tmtbl.custom.properties` property needs to contain the full path leading to the newly created `unitime.properties` file.


Save the file. It should look like this (note the last line).


![Setting up UniTime on Mac](images/installation-mac-custom2.png){:class='screenshot'}

See [http://help.unitime.org/installation#customization](../installation#customization) for more details.


# 6. Start Tomcat


Start the Terminal (Launchpad > Other > Terminal), execute:



```
~/Downloads/apache-tomcat-9.0.90/bin/startup.sh
```




![Setting up UniTime on Mac](images/installation-mac-startup.png){:class='screenshot'}


Now, you should be able to open UniTime at [http://localhost:8080/UniTime](http://localhost:8080/UniTime)


![Setting up UniTime on Mac](images/installation-mac-login1.png){:class='screenshot'}


And log in using the admin user (both username and password is `admin`)


![Setting up UniTime on Mac](images/installation-mac-login2.png){:class='screenshot'}




Tomcat can be stopped the same way, but using the stop.sh script instead.




```
~/Downloads/apache-tomcat-9.0.90/bin/stop.sh
```

# 7. Check the logs for any errors ***(optional step)***


The logs are located in `apache-tomcat-9.0.90/logs` folder.


![Setting up UniTime on Mac](images/installation-mac-logs1.png){:class='screenshot'}


You can use the Utilities > Console app to view the log files.

![Setting up UniTime on Mac](images/installation-mac-logs2.png){:class='screenshot'}

All the UniTime related messages should be placed in the `unitime.log`, but other files (especially the `catalina.out` and `catalina.<DATE>.log`) may contain useful information. If everything started as it should, there should be the following messages in the `unitime.log` file (abbreviated):

```
27-Jun-24 15:55:36.476 [main] INFO  StartupService.afterPropertiesSet> ******* UniTime 4.8.139 build on Tue, 18 Jun 2024 is starting up *******
27-Jun-24 15:55:36.476 [main] INFO  StartupService.afterPropertiesSet>  - Initializing Hibernate ... 
...
27-Jun-24 15:55:41.823 [main] INFO  DatabaseUpdate.<init>> Reading file:/Users/muller/Downloads/apache-tomcat-9.0.90/webapps/UniTime/WEB-INF/lib/timetable.jar!/dbupdate.xml ...
27-Jun-24 15:55:42.052 [main] INFO  util.DatabaseUpdate> Current UniTime database version: 123
27-Jun-24 15:55:42.070 [main] INFO  util.DatabaseUpdate>   Performing UniTime update to version 124 (Instructor Note)
27-Jun-24 15:55:42.127 [main] INFO  util.DatabaseUpdate>     UniTime Database version increased to: 124
27-Jun-24 15:55:42.158 [main] INFO  util.DatabaseUpdate>   Performing UniTime update to version 125 (Solution Export XML)
27-Jun-24 15:55:42.165 [main] INFO  util.DatabaseUpdate>     UniTime Database version increased to: 125
...
27-Jun-24 15:55:48.086 [main] INFO  util.DatabaseUpdate>   Performing UniTime update to version 268 (Access Control Statistics)
27-Jun-24 15:55:48.098 [main] INFO  util.DatabaseUpdate>     UniTime Database version increased to: 268
27-Jun-24 15:55:48.104 [main] INFO  util.DatabaseUpdate>   Performing UniTime update to version 269 (Access Control Statistics Update)
27-Jun-24 15:55:48.132 [main] INFO  util.DatabaseUpdate>     UniTime Database version increased to: 269
27-Jun-24 15:55:48.134 [main] INFO  util.DatabaseUpdate> New UniTime database version: 269
27-Jun-24 15:55:48.139 [main] INFO  StartupService.afterPropertiesSet>  - Creating Message Log Appender ... 
27-Jun-24 15:55:48.145 [main] INFO  StartupService.afterPropertiesSet>  - Initializing Room Availability Service ... 
27-Jun-24 15:55:48.163 [main] INFO  StartupService.afterPropertiesSet>  - Cleaning Logs ...
27-Jun-24 15:55:48.218 [main] INFO  util.LogCleaner> All records older than 14 days deleted from the student sectioning queue (9 records).
27-Jun-24 15:55:48.223 [main] INFO  StartupService.afterPropertiesSet>  - Starting Event Expiration Service ...
27-Jun-24 15:55:48.226 [EventExpirationService] INFO  events.EventExpirationService> Event expiration service started.
27-Jun-24 15:55:48.226 [main] INFO  StartupService.afterPropertiesSet> ******* UniTime 4.8.139 build on Tue, 18 Jun 2024 initialized successfully *******
```