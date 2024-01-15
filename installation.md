---
layout: default
title: UniTime Installation
---
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