---
layout: default
title: UniTime Installation
---
For simplified step by step installation notes, see
- [Setting up UniTime on Linux](https://docs.google.com/document/d/1Nkhlb61rjRY55MaLW44bSMm5-FBqQEPpb0K4DJOOUmM/edit?usp=sharing)
- [Setting up UniTime on Windows](https://docs.google.com/a/unitime.org/document/d/1VCscHsSpazzmsh_DQZiicqOjAda3eX0f4S9oxlll8CY/edit?usp=sharing)
- [Setting up UniTime on Mac](https://docs.google.com/document/d/1y3mKe1accr8qYPIbADqW40fd4HcAYNfAwJpduloGOQ0)

### Table of Contents
{:.no_toc}
* table
{:toc}

## Prerequisites

### Java Development Kit

* If you do not have Java SE (Standard Edition) Development Kit 11 or later already installed, you will need to download and install it from Java SE Downloads first.
    * OpenJDK 11 and 17 are used in development and/or testing.
    * Note: Starting with UniTime 4.8, Java 8 is no longer supported.

### Apache Tomcat

* Download [Apache Tomcat](https://tomcat.apache.org/download-90.cgi)
    * **Versions 8.5 and 9.0 are used for development and/or testing.**
    * Apache Tomcat 10.0 is not supported in UniTime 4.5 or older due to the change from Java EE to Jakarta EE. A special Tomcat 10 compatible build of UniTime is needed.
    * Apache Tomcat 7.0 or earlier is not supported in UniTime 4.6 or later (Servlet 3.1 or later is needed)
* Install Apache Tomcat
    * For more information about Tomcat setup, see this [Tomcat 8.5 Setup User Guide](http://tomcat.apache.org/tomcat-8.5-doc/setup.html) or [Tomcat 9.0 Setup User Guide](https://tomcat.apache.org/tomcat-9.0-doc/setup.html)
    * You might want to set up SSL (HTTPS) access to your tomcat. See [SSL Configuration HOW-TO](http://tomcat.apache.org/tomcat-8.5-doc/ssl-howto.html) for more details.

### MySQL

* Download MySQL from [MySQL Downloads](https://dev.mysql.com/downloads/mysql)
    * MySQL version 8.0 and Oracle version 19c are currently being used in development and testing.
    * You may need to add serverTimezone parameter in the connection string (see [MySQL Time Zone Support](https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html) for more details).
    * **MariaDB is currently not supported.**
* Install MySQL
    * See [MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/) for more details about installation
* Install MySQL JDBC driver
    * The driver can be downloaded from the [Download Connector/J](http://dev.mysql.com/downloads/connector/j/) page. Please make sure you use the same version as your MySQL database.
    * Unzip the downloaded driver if needed and place the mysql-connector-java-8.0.x.jar under the Tomcat/lib folder.

## Installation
* Download the latest UniTime 4.8 distribution from [UniTime Downloads](https://sourceforge.net/projects/unitime/files/UniTime%204.8/)
    * All distributions are platform-independent, distributed in either .zip or .tar.gz format
    * Alternatively, you can download the most recent nightly build from [UniTime Nightly Builds](http://builds.unitime.org/)
* Unzip the archive
```
tar -xvzf unitime-4.8_bld100.tar.gz
```
* Install `timetable` database
    * MySQL installation scripts are located in `doc/mysql` folder of the distribution
    * File `schema.sql` contains the database schema, file `woebegon-data.sql` contains test data (Woebegon College Test Suite, see [Online Demo](https://demo.unitime.org/) for more details).
        * If you want to change the default user name/password, edit the file schema.sql first. The user is created at the very beginning of the script.
    *Timetable database can be created and populated using the `mysql` command-line tool
        * After running `schema.sql`, you need to populate the database either using `woebegon-data.sql` or `blank-data.sql` file
        * When `woebegon-data` are used, you will be able to login into the application using the same credentials as described on our online demo page
        * When `blank-data` are used, there is only administrator account created. Both username and password are admin.
```
mysql -uroot -p -f <schema.sql
mysql -uroot -p <woebegon-data.sql
```
* Deploy UniTime application
    * Copy `web/UniTime.war` to `Tomcat/webapps`, where `Tomcat` is the folder where Tomcat is installed.
        * On unix-based systems (including Mac OS X), java virtual machine that is running tomcat needs to be switched to (headless mode)[https://www.oracle.com/technical-resources/articles/javase/headless.html]. You can do that using JAVA_OPTS environment variable prior to starting tomcat:
```
export JAVA_OPTS="${JAVA_OPTS} -Djava.awt.headless=true"
```
        * Also, you might need to give Tomcat more memory to work with by changing the upper limit on the memory that it can allocate (especially if you are planning not to run any remote solver servers -- see below; default is 64MB). You can do that using JAVA_OPTS environment variable as well:
```
export JAVA_OPTS="${JAVA_OPTS} -Xmx2048m"
```
    * Start tomcat
        * If everything goes well, you should be able to see UniTime application at [http://localhost:8080/UniTime](http://localhost:8080/UniTime) or [https://localhost:8443/UniTime](https://localhost:8443/UniTime) when SSL connector is enabled.
        * If not, please check the tomcat log for any potential problems -- it is located at `Tomcat/logs/catalina.out`
            * Please refer to for a solution [Installation FAQ](timetabling-installation-faq) and/or write us an email to [support@unitime.org](support@unitime.org)
* **Tip:** If you have installed Tomcat on a Linux-based machine from a package (e.g., by running apt-get install tomcat8), you will need to make sure that there is a data folder available within the tomcat directory and that Tomcat has enough permissions to write files in there. This can be accomplished with something like:
```
mkdir /var/lib/tomcat8/data
chown tomcat8 /var/lib/tomcat8/data
```
    * Tomcat configuration (including the  JAVA_OPTS variable) is located in the `/etc/default/tomcat8` file in this case.
* **Tip:** If you are using Tomcat 9 on Ubuntu/Debian, you may need to create a file `/etc/systemd/system/tomcat9.service.d/override.conf` containing the following lines:
```
[Service] ReadWritePaths=/var/lib/tomcat9/data
```
    * This is due to the new sandboxing feature. More details are available at [https://salsa.debian.org/java-team/tomcat9/blob/master/debian/README.Debian](https://salsa.debian.org/java-team/tomcat9/blob/master/debian/README.Debian)

## Upgrade
* Please note that UniTime 4.8 requires Java 11 or later. Java 8 is no longer supported.
* To upgrade an existing UniTime installation, only the new `UniTime.war` file should be placed in the `Tomcat/webapps` folder instead of the existing one. All the necessary changes to the database are done automatically during the first deployment. The safest way to do so is as follows:
1. Stop tomcat
2. Backup the existing database (e.g., using mysqldump on MySQL or exp on Oracle)
3. In `Tomcat/webapps`, remove `UniTime` folder and replace the existing `UniTime.war` with the new one
4. Delete the content of `Tomcat/work` folder.
5. Start the tomcat
* If you are using remove solver servers, the appropriate JARs need to be updated as well.
    * Some HQL reports may need to be updated due to the Hibernate upgrade, e.g.,
    * table = id no longer works (e.g., Session = %SESSION% must be changed to Session.uniqueId = %SESSION%)
    * is true needs to be changed to x = true
    * function BIT_AND needs to be changed to BITAND
    * InstructionalOffering.coordinators needs to be changed to InstructionalOffering.offeringCoordinators
    * Assignment.classId needs to be changed to Assignment.clazz.uniqueId
    * CourseOffering.isControl = 1 needs to be changed to CourseOffering.isControl = true
    * mod(x, n) may need to be changed to mod(cast(x as int), n)
    * sysdate - :days (where :days is an integer) may need to be changed to sysdate - numtodsinterval(:days, ‘day’) (Oracle)
* Some Scripts may need to be updated due to the Hibernate upgrade, e.g,
    * Query.setLong, setString, setDate, etc., needs to be changed to setParameter
    * QueueIn/QueueOut.setXml/getXML now takes a string (use setDocument/getDocument for XML access)
* See [UniTime 4.8 release notes](https://builds.unitime.org/UniTime4.8/Release-Notes.xml) for other changes.

## Customization

* Custom Properties
    * There are a lot of properties that are defined in file [application.properties](https://github.com/UniTime/unitime/blob/master/JavaSource/application.properties) that is located in `timetable.jar` which is located in `UniTime.war` at `WEB-INF/lib`. These properties can be changed in one of the following ways:
1. By providing a custom property file, this file should be named `custom.properties` and located in `UniTime.war` at `WEB-INF/classes`.
        * Alternatively, the custom property file can be located somewhere else, with system property tmtbl.custom.properties pointing to it.
2. By adding and/or changing the appropriate properties directly in the UniTime application -- see Administration / Defaults / Configuration menu item when logged in as administrator.
3. By adding these properties in `Tomcat/conf/catalina.properties`
4. By providing JVM that is running tomcat with the appropriate system properties, for instance:
```
export JAVA_OPTS="${JAVA_OPTS} -Dtmtbl.title=Timetabling Demo"
export JAVA_OPTS="${JAVA_OPTS} -Dtmtbl.custom.properties=/etc/default/unitime.properties
```
* **Tip:** Name the custom properties file `Tomcat/conf/unitime.properties` and put all the properties you need in there. For `UniTime` to use the file, add the following line to `Tomcat/conf/catalina.properties`
```
tmtbl.custom.properties=${catalina.base}/conf/unitime.properties
```
* If the same property is defined on multiple places, the first one from the following order will be taken:
    1. UniTime Configuration (Administration / Defaults / Configuration menu item)
    2. System property (`-Dproperty=value`, or defined in `Tomcat/conf/catalina.properties`)
    3. File **custom.properties** (`UniTime.war/WEB-INF/classes/custom.properties` or as defined by `tmtbl.custom.properties` system property)
    4. File **application.properties** (`UniTime.war/WEB-INF/lib/timetable.jar/application.properties`)

* Database Connection
    * The database connection can be changed using custom properties. However, please note that these properties cannot be defined using the UniTime application (Administration / Defaults / Configuration menu item) since the database connection needs to be configured before the database can be accessed. For instance, custom.properties file can contain the following:
```
# MySQL Configuration Example
connection.url=jdbc:mysql://localhost:3306/timetable?serverTimezone=Europe/Prague
connection.username=timetable
connection.password=unitime
connection.driver_class=com.mysql.jdbc.Driver
dialect=org.hibernate.dialect.MySQLDialect
tmtbl.uniqueid.generator=org.hibernate.id.TableHiLoGenerator
default_schema=timetable
```
* See [LDAP Authentication / Lookup](LDAP) page for notes about LDAP integration.
* See [Customizations](customizations) page for notes about the custom styling (branding) of the UniTime application.