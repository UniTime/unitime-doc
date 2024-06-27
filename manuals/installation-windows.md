---
layout: manual
title: Setting up UniTime on Windows
version: 4.8
---

### Table of Contents
{:.no_toc}
* table
{:toc}


# 1. Install Oracle Java 21


Download JDK 21 from [hhttps://www.oracle.com/java/technologies/downloads](https://www.oracle.com/java/technologies/downloads/#jdk21-windows) (a file named like jdk-21_windows-x64_bin.exe), start it up and follow the installation instructions.

![Intalling Java on Windows](images/installation-windows-java1.png){:class='screenshot'}

Hit Next

![Intalling Java on Windows](images/installation-windows-java2.png){:class='screenshot'}

Leave as it is, hit Next

![Intalling Java on Windows](images/installation-windows-java3.png){:class='screenshot'}

Wait for the installation to finish...

![Intalling Java on Windows](images/installation-windows-java4.png){:class='screenshot'}

Hit Close

# 2. Install MySQL 8.4

Download MySQL Community Server from [https://dev.mysql.com/downloads/mysql](https://dev.mysql.com/downloads/mysql) (a file named like mysql-8.4.0-winx64.msi), start it up and follow the installation instructions.

![Intalling MySQL on Windows](images/installation-windows-mysql1.png){:class='screenshot'}

Click Next

![Intalling MySQL on Windows](images/installation-windows-mysql2.png){:class='screenshot'}

Accept license terms, click Next

![Intalling MySQL on Windows](images/installation-windows-mysql3.png){:class='screenshot'}

Choose Typical

![Intalling MySQL on Windows](images/installation-windows-mysql4.png){:class='screenshot'}

Click Install

![Intalling MySQL on Windows](images/installation-windows-mysql5.png){:class='screenshot'}

Wait for the installation to finish...

![Intalling MySQL on Windows](images/installation-windows-mysql6.png){:class='screenshot'}

Leave Run MySQL Configurator checked, click Finish

![Intalling MySQL on Windows](images/installation-windows-mysql7.png){:class='screenshot'}

In the MySQL Configurator, click Next

![Intalling MySQL on Windows](images/installation-windows-mysql8.png){:class='screenshot'}

Leave as is, click Next

![Intalling MySQL on Windows](images/installation-windows-mysql9.png){:class='screenshot'}

Leave as is, click Next

![Intalling MySQL on Windows](images/installation-windows-mysql10.png){:class='screenshot'}

Fill in a MySQL Root Password (can be different from any other password). Click Next

![Intalling MySQL on Windows](images/installation-windows-mysql11.png){:class='screenshot'}

Leave as is, click Next

![Intalling MySQL on Windows](images/installation-windows-mysql12.png){:class='screenshot'}

Leave as is, click Next

![Intalling MySQL on Windows](images/installation-windows-mysql13.png){:class='screenshot'}

Leave as is, click Next

![Intalling MySQL on Windows](images/installation-windows-mysql14.png){:class='screenshot'}

Click Execute

![Intalling MySQL on Windows](images/installation-windows-mysql15.png){:class='screenshot'}

Wait for the installation to finish...

![Intalling MySQL on Windows](images/installation-windows-mysql16.png){:class='screenshot'}

Click Next

![Intalling MySQL on Windows](images/installation-windows-mysql17.png){:class='screenshot'}

Click Finish

# 3. Install Apache Tomcat 9.0

**Note:** Tomcat 10 or later are currenrtly not supported!

Download Apache Tomcat 9.0 from [https://tomcat.apache.org/download-90.cgi](https://tomcat.apache.org/download-90.cgi) (choose the 32-bit/64-bit Windows Service Installer option, a file named like apache-tomcat-9.0.90.exe), start it up and follow the installation instructions.

![Intalling Tomcat on Windows](images/installation-windows-tomcat1.png){:class='screenshot'}

Click Next

![Intalling Tomcat on Windows](images/installation-windows-tomcat2.png){:class='screenshot'}

Accept the license by clicking I Agree

![Intalling Tomcat on Windows](images/installation-windows-tomcat3.png){:class='screenshot'}

Leave as is, click Next

![Intalling Tomcat on Windows](images/installation-windows-tomcat4.png){:class='screenshot'}

Leave as is, click Next

![Intalling Tomcat on Windows](images/installation-windows-tomcat5.png){:class='screenshot'}

Leave as is, click Next

![Intalling Tomcat on Windows](images/installation-windows-tomcat6.png){:class='screenshot'}

Leave as is, click Next

![Intalling Tomcat on Windows](images/installation-windows-tomcat7.png){:class='screenshot'}

Wait for the installation to finish. Click Finish


Open Apache Tomcat configuration (Start > All Programs > Apache Tomcat 9.0 > Configure Tomcat). On the Java tab, set the Maximum memory pool to at least 1024 MB. If the menu option does not work, open the File Explorer, navigate to C:\Program Files\Apache Software Foundation\Tomcat 9.0\bin, and open Tomcat9w.

![Intalling Tomcat on Windows](images/installation-windows-tomcat8.png){:class='screenshot'}

This will open the Apache Tomcat 9.0 Tomcat9 Properties dialog.

![Intalling Tomcat on Windows](images/installation-windows-tomcat9.png){:class='screenshot'}

Select Java tab, and change **maximum memory pool** to at least 1024 MB. Click Apply and OK.

# 4. Install MySQL JDBC driver

Download MySQL Connector/J driver from [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/) (choose Platform Independent ZIP Archive, a file named like `mysql-connector-j-8.4.0.zip`). Unzip the downloaded file (right-click the downloaded file and choose Extract All…). In `Downloads\mysql-connector-j-8.4.0`, copy the extracted `mysql-connector-j-8.4.0.jar` into `C:\Program Files\Apache Software Foundation\Tomcat 9.0\lib`.

![Intalling Tomcat on Windows](images/installation-windows-tomcat10.png){:class='screenshot'}


# 5. Install UniTime


Download UniTime from [https://github.com/UniTime/unitime/releases/latest](https://github.com/UniTime/unitime/releases/latest) (a file named like unitime-4.8_bld139.zip) and unzip it (right click the downloaded file and choose Extract All..).

## 5a. Create and populate the timetable database

Start the command prompt (Start > All Programs > Accessories > Command Prompt), execute:


```
mysql -u root -p -f <Downloads\unitime4.8_bld139\doc\mysql\schema.sql
mysql -u root -p <Downloads\unitime-4.8_bld139\doc\mysql\woebegon-data.sql
```

![Creating the database on Windows](images/installation-windows-database.png){:class='screenshot'}

When prompted, use the MySQL root user password as provided in step 2.

If you get "`mysql` is not recognized as an internal or external command, operable program or batch file." error, use `"c:\Program Files\MySQL\MySQL Server 8.4\bin\mysql.exe"` instead as on the above screenshot.

## 5b. Deploy the UniTime application

Copy `web\UniTime.war` from the unzipper UniTime archive to `C:\Program Files\Apache Software Foundation\Tomcat 9.0\webapps`

![Deploying UniTime.war on Windows](images/installation-windows-deploy.png){:class='screenshot'}

## 5c. Create UniTime custom properties file ***(optional step)***

Create `C:\Program Files\Apache Software Foundation\Tomcat 9.0\conf\unitime.txt` file (e.g., by using + New in the File Explorer and selecting Text Document)

![Custom properties on Windows](images/installation-windows-custom1.png){:class='screenshot'}

Open `catalina.properties` in the same folder, add the following line and save it again.

```
tmtbl.custom.properties=C:\\Program Files\\Apache Software Foundation\\Tomcat 9.0\\conf\\unitime.txt
```

![Custom properties on Windows](images/installation-windows-custom2.png){:class='screenshot'}

See [http://help.unitime.org/installation#customization](../installation#customization) for more details.


# 6. Restart Tomcat


Open Apache Tomcat configuration (Start > All Programs > Apache Tomcat 9.0 > Configure Tomcat).

On the General tab, hit Stop if the tomcat is already running. Once stopped, hit Start (you can change the Startup type to Automatic if you with Apache Tomcat to start automatically after Windows restart).

![Restarting UniTime on Windows](images/installation-windows-restart.png){:class='screenshot'}

The Tomcat is running (you can stop the Tomcat here as well). Hit OK to close the dialog.

Now, you should be able to open UniTime at [http://localhost:8080/UniTime](http://localhost:8080/UniTime)

![Logging into UniTime on Windows](images/installation-windows-login.png){:class='screenshot'}

And log in using the admin user (both username and password is admin)

![Logging into UniTime on Windows](images/installation-windows-success.png){:class='screenshot'}

# 7. Check the logs for any errors ***(optional step)***

The logs are located at `C:\Program Files\Apache Software Foundation\Tomcat 9.0\logs`

![UniTime Logs on Windows](images/installation-windows-log1.png){:class='screenshot'}

All the UniTime related messages should be placed in the `unitime.log`, but other files (especially the `catalina.<DATE>.log`, `tomcat9-stderr.<DATE>.log`, and `tomcat9-stdout.<DATE>.log`) may contain useful information. If everything started as it should, there should be the following messages in the unitime.log file (abbreviated):

![UniTime Logs on Windows](images/installation-windows-log2.png){:class='screenshot'}