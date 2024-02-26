---
layout: default
title: UniTime Installation
---
For simplified step by step installation notes, see
- [Setting up UniTime on Linux](manuals/installation-linux)
- [Setting up UniTime on Windows](manuals/installation-windows)
- [Setting up UniTime on Mac](manuals/installation-mac)

### Table of Contents
{:.no_toc}
* table
{:toc}

## Prerequisites

### Java Development Kit

If you do not have Java SE (Standard Edition) Development Kit 8 or later already installed, you will need to download and install it from Java SE Downloads first.
* OpenJDK 8, 11 and 17 are used in development and/or testing.

### Apache Tomcat

Download [Apache Tomcat](https://tomcat.apache.org/download-90.cgi)
* **Versions 8.5 and 9.0 are used for development and/or testing.**
* Apache Tomcat 10.0 is not supported in UniTime 4.5 or older due to the change from Java EE to Jakarta EE. A special Tomcat 10 compatible build of UniTime is needed.
* Apache Tomcat 7.0 or earlier is not supported in UniTime 4.6 or later (Servlet 3.1 or later is needed)

Install Apache Tomcat
* For more information about Tomcat setup, see this [Tomcat 8.5 Setup User Guide](http://tomcat.apache.org/tomcat-8.5-doc/setup.html) or [Tomcat 9.0 Setup User Guide](https://tomcat.apache.org/tomcat-9.0-doc/setup.html)
* You might want to set up SSL (HTTPS) access to your tomcat. See [SSL Configuration HOW-TO](http://tomcat.apache.org/tomcat-8.5-doc/ssl-howto.html) for more details.

### MySQL

Download MySQL from [MySQL Downloads](https://dev.mysql.com/downloads/mysql)
* MySQL version 8.0 and Oracle version 19c are currently being used in development and testing.
* You may need to add serverTimezone parameter in the connection string (see [MySQL Time Zone Support](https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html) for more details).
* **MariaDB is currently not supported.**

Install MySQL
* See [MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/) for more details about installation

Install MySQL JDBC driver
* The driver can be downloaded from the [Download Connector/J](http://dev.mysql.com/downloads/connector/j/) page. Please make sure you use the same version as your MySQL database.
* Unzip the downloaded driver if needed and place the mysql-connector-java-8.0.x.jar under the Tomcat/lib folder.

## Installation
Download the latest UniTime 4.7 distribution from [UniTime Downloads](https://sourceforge.net/projects/unitime/files/UniTime%204.7/)
* All distributions are platform-independent, distributed in either .zip or .tar.gz format
* Alternatively, you can download the most recent nightly build from [UniTime Nightly Builds](https://builds.unitime.org/)

Unzip the archive
```
tar -xvzf unitime-4.7_bld100.tar.gz
```

Install `timetable` database
* MySQL installation scripts are located in `doc/mysql` folder of the distribution
* File `schema.sql` contains the database schema, file `woebegon-data.sql` contains test data (Woebegon College Test Suite, see [Online Demo](https://demo.unitime.org/) for more details).
	* If you want to change the default user name/password, edit the file schema.sql first. The user is created at the very beginning of the script.
* Timetable database can be created and populated using the `mysql` command-line tool
	* After running `schema.sql`, you need to populate the database either using `woebegon-data.sql` or `blank-data.sql` file
	* When `woebegon-data` are used, you will be able to login into the application using the same credentials as described on our online demo page
	* When `blank-data` are used, there is only administrator account created. Both username and password are admin.
```
mysql -uroot -p -f <schema.sql
mysql -uroot -p <woebegon-data.sql
```

Deploy UniTime application
* Copy `web/UniTime.war` to `Tomcat/webapps`, where `Tomcat` is the folder where Tomcat is installed.
	* On unix-based systems (including Mac OS X), java virtual machine that is running tomcat needs to be switched to (headless mode)[https://www.oracle.com/technical-resources/articles/javase/headless.html]. You can do that using JAVA_OPTS environment variable prior to starting tomcat:
```
export JAVA_OPTS="${JAVA_OPTS} -Djava.awt.headless=true"
```
	* Also, you might need to give Tomcat more memory to work with by changing the upper limit on the memory that it can allocate (especially if you are planning not to run any remote solver servers -- see below; default is 64MB). You can do that using JAVA_OPTS environment variable as well:
```
export JAVA_OPTS="${JAVA_OPTS} -Xmx2048m"
```

Start tomcat
* If everything goes well, you should be able to see UniTime application at [http://localhost:8080/UniTime](http://localhost:8080/UniTime) or [https://localhost:8443/UniTime](https://localhost:8443/UniTime) when SSL connector is enabled.
* If not, please check the tomcat log for any potential problems -- it is located at `Tomcat/logs/catalina.out`
	* Please refer to for a solution [Installation FAQ](timetabling-installation-faq) and/or write us an email to [support@unitime.org](support@unitime.org)

**Tip:** If you have installed Tomcat on a Linux-based machine from a package (e.g., by running apt-get install tomcat8), you will need to make sure that there is a data folder available within the tomcat directory and that Tomcat has enough permissions to write files in there. This can be accomplished with something like:
```
mkdir /var/lib/tomcat8/data
chown tomcat8 /var/lib/tomcat8/data
```
* Tomcat configuration (including the  JAVA_OPTS variable) is located in the `/etc/default/tomcat8` file in this case.

**Tip:** If you are using Tomcat 9 on Ubuntu/Debian, you may need to create a file `/etc/systemd/system/tomcat9.service.d/override.conf` containing the following lines:
```
[Service] ReadWritePaths=/var/lib/tomcat9/data
```
* This is due to the new sandboxing feature. More details are available at [https://salsa.debian.org/java-team/tomcat9/blob/master/debian/README.Debian](https://salsa.debian.org/java-team/tomcat9/blob/master/debian/README.Debian)

## Upgrade
To upgrade an existing UniTime installation, only the new `UniTime.war` file should be placed in the `Tomcat/webapps` folder instead of the existing one. All the necessary changes to the database are done automatically during the first deployment. The safest way to do so is as follows:
1. Stop tomcat
2. Backup the existing database (e.g., using mysqldump on MySQL or exp on Oracle)
3. In `Tomcat/webapps`, remove `UniTime` folder and replace the existing `UniTime.war` with the new one
4. Delete the content of `Tomcat/work` folder.
5. Start the tomcat

See [UniTime 4.7 release notes](https://builds.unitime.org/UniTime4.7/Release-Notes.xml) for other changes.

## Customization

#### Custom Properties
There are a lot of properties that are defined in file [application.properties](https://github.com/UniTime/unitime/blob/master/JavaSource/application.properties) that is located in `timetable.jar` which is located in `UniTime.war` at `WEB-INF/lib`. These properties can be changed in one of the following ways:
1. By providing a custom property file, this file should be named `custom.properties` and located in `UniTime.war` at `WEB-INF/classes`.
2. Alternatively, the custom property file can be located somewhere else, with system property `tmtbl.custom.properties` pointing to it.
3. By adding and/or changing the appropriate properties directly in the UniTime application -- see Administration / Defaults / Configuration menu item when logged in as administrator.
4. By adding these properties in `Tomcat/conf/catalina.properties`
5. By providing JVM that is running tomcat with the appropriate system properties, for instance:
```
export JAVA_OPTS="${JAVA_OPTS} -Dtmtbl.title=Timetabling Demo"
export JAVA_OPTS="${JAVA_OPTS} -Dtmtbl.custom.properties=/etc/default/unitime.properties
```

**Tip:** Name the custom properties file `Tomcat/conf/unitime.properties` and put all the properties you need in there. For `UniTime` to use the file, add the following line to `Tomcat/conf/catalina.properties`
```
tmtbl.custom.properties=${catalina.base}/conf/unitime.properties
```

If the same property is defined on multiple places, the first one from the following order will be taken:
1. UniTime Configuration (Administration / Defaults / Configuration menu item)
2. System property (`-Dproperty=value`, or defined in `Tomcat/conf/catalina.properties`)
3. File `custom.properties` (`UniTime.war/WEB-INF/classes/custom.properties` or as defined by `tmtbl.custom.properties` system property)
4. File `application.properties` (`UniTime.war/WEB-INF/lib/timetable.jar/application.properties`)

#### Database Connection
The database connection can be changed using custom properties. However, please note that these properties cannot be defined using the UniTime application (Administration / Defaults / Configuration menu item) since the database connection needs to be configured before the database can be accessed. For instance, custom.properties file can contain the following:
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

#### Other
* See [LDAP Authentication / Lookup](LDAP) page for notes about LDAP integration.
* See [Customizations](customizations) page for notes about the custom styling (branding) of the UniTime application.

## Remote Solver Server(s)

By default, all timetabling problems are solved within the application (using the same Java Virtual Machine), however, especially for bigger institutions, it might be desired to solve the timetabling problems by one or more separate solver servers.

All the necessary libraries are in the solver folder of the distribution except the JDBC driver. For MySQL 8.x download [mysql-connector-java-8.0.33.jar](https://repo1.maven.org/maven2/com/mysql/mysql-connector-j/8.0.33/mysql-connector-j-8.0.33.jar),  or for Oracle download [ojdbc8.jar](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html). If a different version of the driver is downloaded, rename it to mysql-connector-java.jar or ojdbc8.jar.

Place the JDBC driver in the solver directory (same location as the timetable.jar), for instance:
```
curl https://repo1.maven.org/maven2/com/mysql/mysql-connector-j/8.0.33/mysql-connector-j-8.0.33.jar --output solver/mysql-connector-java.jar
```

To run a remote solver, do:
```
java -Xmx2g -Dtmtbl.custom.properties=custom.properties -jar solver/timetable.jar
```

File `custom.properties` should contain all the custom parameters needed for the starting up the server (e.g., database connection properties, if different from the defaults). It is usually the same as the one used on the Tomcat, except the jgroups.tcp.address property (see below). The load is automatically and seamlessly balanced between the remote solvers. The remote solver server also automatically reconnects itself when the web server is restarted. When the remote solver is shut down, all active timetabling instances are backed up and restored when the solver server is started again. The following properties need to be set in the `custom.properties` file. Please note that all these properties need to be set on the Tomcat side as well.
```
jgroups.tcp.address=127.0.0.1
```
IP address of the machine that is using this configuration file. This property should be different on each machine; the remaining properties are usually the same for all the UniTime instances (Tomcats as well as remote solver servers). If the property is set to 127.0.0.1 or localhost, the server will not be able to accept remote connections -- use only if all the instances are running on the same machine!
```
unitime.solver.cluster=true
```

This property enables the Solver cluster. This cluster is used for RPCs between the Tomcat(s) and the remote solver server(s). Communication between UniTime instances is done using [JGroups](http://www.jgroups.org/).
```
unitime.solver.port=7800
```

Default communication port for the Solver cluster. If the given port is taken (e.g., there are running multiple remote solver server(s) on the same machine), the next one available will be used instead.
```
unitime.solver.initial_hosts=127.0.0.1[7800]
```

By default, TCP ping discovery is used to form a cluster. The above parameter defines a comma-separated list of machines (and their communication ports) on which a UniTime instance may be running. It does not necessarily need to have all the possible IP addresses; usually, it is set to the IP addresses of the Tomcat server(s) running UniTime.
```
unitime.solver.jgroups.config=solver-jgroups-tcp.xml
```


An alternative JGroups configuration file can be provided with this property. The default configuration file is available [here](https://github.com/UniTime/unitime/tree/master/JavaSource/solver-jgroups-tcp.xml).

* The remote solvers can be managed in the UniTime application; see Administration > Solver > [Manage Solvers](manage-solvers) menu item when logged in as an administrator.

## Having Multiple Tomcats (Clustering)

With UniTime 4.0, it is possible to run multiple instances of UniTime on a cluster of Tomcats and/or remote solver servers. Besides the Solver cluster and Enrollment cluster, it is also possible to form a Hibernate cluster that is used to replicate Hibernate L2 cache. The following properties can be used to configure the Hibernate cluster.
```
unitime.hibernate.cluster=true
```

This property enables the Hibernate cluster. This cluster is used for replication of Hibernate second level cache between multiple UniTime instances.
```
unitime.hibernate.port=7833
```

Default communication port for the Hibernate cluster. If the given port is taken (e.g., there are running multiple remote solver server(s) on the same machine), the next one available will be used instead.
```
unitime.hibernate.initial_hosts=127.0.0.1[7833]
```

By default, TCP ping discovery is used to form a cluster. The above parameter defines a comma-separated list of machines (and their communication ports) on which a UniTime instance may be running. It does not necessarily need to have all the possible IP addresses; usually, it is set to the IP addresses of the Tomcat server(s) running UniTime.
```
unitime.hibernate.jgroups.config=hibernate-jgroups-tcp.xml
```

An alternative JGroups configuration file can be provided with this property. The default configuration file is available [here](https://github.com/UniTime/unitime/tree/master/JavaSource/hibernate-jgroups-tcp.xml).

Please note that Hibernate cluster is only needed when there are two or more Tomcats running UniTime. Remote solver servers have the L2 cache disabled and hence no need to connect to the Hibernate cluster.

## Using Oracle Database

Here are some notes about using Oracle Database

The following custom properties need to be set (connection URL, username, and password may vary)
```
# Oracle Configuration Example
connection.url=jdbc:oracle:thin:@localhost:1521:xe
connection.username=timetable
connection.password=unitime
connection.driver_class=oracle.jdbc.driver.OracleDriver
dialect=org.hibernate.dialect.OracleDialect
tmtbl.uniqueid.generator=org.hibernate.id.SequenceGenerator
```

If the schema is different from `timetable`, the `default_schema` property needs to be changed as well
```
default_schema=timetable
```

File `ojdbc8.jar` (or later) needs to be copied either to Tomcat/lib or to Tomcat/webapps/UniTime/WEB-INF/lib. This file can be downloaded, e.g., from [Oracle JDBC Drivers](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)

Oracle installation scripts are located in doc/oracle folder of the distribution
* Alternatively, the database can be imported using `imp` tool and the [woebegon.dat](https://github.com/UniTime/unitime/blob/master/Documentation/Database/Oracle/woebegon.dat?raw=true) from the GitHub.
```
imp timetable/###### file=woebegon.dat full=y
```

User timetable needs to be created first, e.g., using sqlplus
```
sqlplus system
create user timetable identified by ######; grant dba to timetable; exit
```

## Using PostgreSQL

Here are some notes about using PostgreSQL, for more details, please see the [Migrating to PostgreSQL](manuals/postgresql-migration) document.

Install PostgreSQL 12.0 or later from [https://www.postgresql.org/download](https://www.postgresql.org/download) (using the default port 5432, and a custom password)

Create timetable user and timetable database, using the same name and credentials as the default UniTime database:
```
createuser --interactive --pwprompt -U postgres
Enter name of role to add: timetable
Enter password for new role: unitime
Enter it again: unitime
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n
Password: <password provided during install>
createdb timetable -U timetable -O timetable
Password: unitime
```

Populate the timetable database, using this [timetable.sql](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Database/PostgreSQL/timetable.sql) file (Documentation/Database/PostgreSQL/timetable.sql in [https://github.com/UniTime/unitime](https://github.com/UniTime/unitime))
```
psql -U timetable <timetable.sql
```

Download JDBC Driver from [https://jdbc.postgresql.org/download.html](https://jdbc.postgresql.org/download.html) and place it to Tomcat/lib (e.g., postgresql-42.2.8.jar)

Change UniTime connection properties. The following custom properties need to be set (connection URL, username, password may vary)
```
# PostgreSQL Configuration Example
connection.url=jdbc:postgresql://localhost:5432/timetable
connection.driver_class=org.postgresql.Driver
dialect=org.hibernate.dialect.PostgreSQLDialect
connection.username=timetable
connection.password=unitime
default_schema=timetable
hibernate.dbcp.validationQuery=select 1
hibernate.globally_quoted_identifiers=true
```

Start UniTime, and check the logs for any errors.