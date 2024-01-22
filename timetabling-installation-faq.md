---
layout: default
title: Timetabling Installation FAQ
---


## Q1: How to enable debug logging


 To enable debug logging from UniTime, add the following lines to Tomcat/conf/catalina.properties
```
log4j.appender.unitimeLogFile=org.apache.log4j.DailyRollingFileAppender
```
```
log4j.appender.unitimeLogFile.File=${catalina.base}/logs/unitime-debug.log
```
```
log4j.appender.unitimeLogFile.DatePattern='.'yyyy-MM-dd
```
```
log4j.appender.unitimeLogFile.Append=true
```
```
log4j.appender.unitimeLogFile.layout=org.apache.log4j.PatternLayout
```
```
log4j.appender.unitimeLogFile.layout.ConversionPattern=[%-d{MM/dd/yy HH:mm:ss}] %-6p %c{1} -> %m%n
```
```
log4j.logger.org.unitime=DEBUG, unitimeLogFile
```
```
log4j.logger.net.sf.cpsolver=DEBUG, unitimeLogFile
```


 After Tomcat is restarted, all UniTime related log messages will be written to Tomcat/logs/unitime-debug.log.

## Q2: The session factory has not been initialized (or an error occurred during initialization).


 The reason why session factory failed to initialize is usually listed in the tomcat log. It is located at Tomcat/logs/catalina.out, Tomcat/logs/stdout.log, or in Tomcat/logs/unitime-debug.log (if debug logging is enabled, see Q0 above).


 If everything goes right, you should be able to see the following messages in the log:
```
[11/06/07 17:03:45] INFO logMessage -> *** Initializing Timetabling Application : START ***
```
```
[11/06/07 17:03:45] INFO logMessage -> - Initializing Debugger ...
```
```
[11/06/07 17:03:45] INFO load -> Reading file:/Library/Tomcat/webapps/UniTime/WEB-INF/lib/timetable.jar!/application.properties ...
```
```
[11/06/07 17:03:45] INFO logMessage -> - Initializing Hibernate ...
```
```
[11/06/07 17:03:47] INFO ConnectionProviderFactory -> Initializing connection provider: org.unitime.commons.hibernate.connection.DBCPConnectionProvider
```
```
[11/06/07 17:03:47] INFO Dialect -> Using dialect: org.hibernate.dialect.MySQLInnoDBDialect
```
```
[11/06/07 17:03:47] INFO TransactionFactoryFactory -> Using default transaction strategy (direct JDBC transactions)
```
```
[11/06/07 17:03:47] INFO TransactionManagerLookupFactory -> No TransactionManagerLookup configured (in JTA environment, use of read-write or transactional second-level cache is not recommended)
```
```
[11/06/07 17:03:47] INFO ASTQueryTranslatorFactory -> Using ASTQueryTranslatorFactory
```
```
[11/06/07 17:03:47] INFO SessionFactoryImpl -> building session factory
```
```
[11/06/07 17:03:48] INFO run -> InfoCache cleanup thread started.
```
```
[11/06/07 17:03:51] INFO SessionFactoryObjectFactory -> Not binding factory to JNDI, no JNDI name configured
```
```
[11/06/07 17:03:51] INFO UpdateTimestampsCache -> starting update timestamps cache at region: org.hibernate.cache.UpdateTimestampsCache
```
```
[11/06/07 17:03:51] INFO StandardQueryCache -> starting query cache at region: org.hibernate.cache.StandardQueryCache
```
```
[11/06/07 17:03:51] INFO logMessage -> - Initializing Solver Register ...
```
```
[11/06/07 17:03:51] INFO SolverRegisterService -> service started
```
```
[11/06/07 17:03:51] INFO logMessage -> *** Timetabling Application : Initializing DONE ***
```


 If not, please refer to the following FAQs and/or write us an email to [support@unitime.org](mailto:support@unitime.org). Please, do not forget to attach the tomcat log.

## Q3: Untrusted apps are not allowed to connect to or launch Window Server before login.


 If you see the above message (or similar) in the tomcat log, the problem can be easily fixed by setting Java system property java.awt.headless to true. You can do this by adding the following line in Tomcat/conf/catalina.properties
```
java.awt.headless=true
```


 prior to starting Tomcat.

## Q4: Table APPLICATION_CONFIG or USERS not found.


 On Lynux based systems, MySQL is case sensitive on table names by default. To change this, add the following line to the /etc/my.cnf file. This forces MySQL to translate all table names to lowercase before executing the statement.
```
lower_case_table_names=1
```

## Q5: Access denied for user 'timetable'@'localhost'


 Was the user timetable created? Was there any error/message printed during the creation of the timetable database (execution of file schema.sql)? Are you using the default password (unitime)?


 You can verify some of that by checking the content of table mysql.user (there should be a line withuser=timetable). You can also try to connect to the database as timetable user using mysql tool with the following options (also trying to use the same port and protocol as the UniTime application):
```
mysql --user=timetable --password=unitime --port=3306 --host=localhost --protocol=TCP timetable
```


 If the localhost as the host for the timetable user does not work, try 127.0.0.1 or without it (which usually creates % as host -- that should work as any host, but usually does not). Also, you should post "flush privileges" after any change to make sure MySQL authentication knows about it.


 ```create user timetable@`127.0.0.1` identified by 'unitime';```


 ```grant all on timetable.* to timetable@`127.0.0.1`;```
```
create user timetable dentified by 'unitime';
```
```
grant all on timetable.* to timetable;
```
```
flush privileges;
```


 So, you would have the following three timetable users in the user table.
```
mysql> select user,host,password from mysql.user where user = 'timetable';
```
```
+-----------+-----------+-------------------------------------------+
```
```
| user      | host      | password                                  |
```
```
+-----------+-----------+-------------------------------------------+
```
```
| timetable | %         | *2E46E61A1C47ADC309CADC6DF8D89654F013D3DD |
```
```
| timetable | localhost | *2E46E61A1C47ADC309CADC6DF8D89654F013D3DD |
```
```
| timetable | 127.0.0.1 | *2E46E61A1C47ADC309CADC6DF8D89654F013D3DD |
```
```
+-----------+-----------+-------------------------------------------+
```
```
3 rows in set (0.00 sec)
```


 The host matching / restrictions is sometimes a pain with MySQL. The localhost usually works, however not 100%.


 You may also need to check that MySQL allows for TCP/IP connections. TCP/IP connections are disabled when MySQL demon runs with skip-networking option.

## Q6: Authentacation Failed


 Is the table timetable.**users** populated? If there are no row, it is likely because you have not run blank-data.sql or woebegon-data.sql after running schema.sql during the installation.


 Besides of this, there should be a line in **timetable_manager** table with **external_uid** column set to 1 (i.e., there is a timetabling manager associated with the user admin). There should be also a line in **tmtbl_mgr_to_roles** table linking the timetabling manager with an administrator role (**roles** table). Also, there should be a line in the **sessions** table.


 Is there any error in the tomcat's log? If not, please enable JAAS debug logging by adding the following line in Tomcat/conf/catalina.properties
```
log4j.logger.org.unitime.timetable.authenticate.jaas=DEBUG
```


 Now, when you try to login (after restarting tomcat), there should be some messages in the log showing that the correct authentication module is used (message " Performing db authentication ...") and explaining why the login failed.


 There is a possibility that a password hash is computed differently due to a use of a different Java or operation system (we are using MD5 encoding provided by Java class java.security.MessageDigest). If the password is incorrect, there should be the following messages in the log (when JAAS debugging is enabled):
```
Performing db authentication ...
```
```
Db authentication failed ...
```
```
ERROR execute -> Login Failure: all modules ignored
```


 In such a case, please generate a new password hash using solver/timetable.jar that is a part of the UniTime distribution (solver folder), i.e., execute:
```
java -cp solver/timetable.jar org.unitime.timetable.authenticate.jaas.DbAuthenticateModule admin
```


 It just prints one string which is the hash of the given argument admin, in my case, it is "ISMvKXpXpadDiUoOSoAfww==". This string needs to be set as password in the users table, i.e.,
```
update timetable.users set password='ISMvKXpXpadDiUoOSoAfww==' where username='admin';
```
```
commit;
```

## Q7: Not enough resources to create a solver instance, please try again later.


 You need to increase the memory limit for the tomcat (in order to prevent OutOfMemory exceptions, solver refuses to start unless there are 200MB available, which is an estimated size for solving of a problem with about 1000 classes). To increase the memory limit, you can for instance add -Xmx512m to JAVA_OPTS environmental variable before starting tomcat (this will allow tomcat to allocate up to 512MB of memory, default is 64MB):


 On Unix/Linux/MacOS:
```
export JAVA_OPTS="${JAVA_OPTS} -Xmx512m"
```


 On windows:
```
set JAVA_OPTS=%JAVA_OPTS% -Xmx512m
```


 Alternatively, the limit on variable memory can be changed by setting the application property tmtbl.solver.mem_limit. This can be done using JAVA_OPTS environment variable before starting tomcat:


 On Unix/Linix/MacOS:
```
export JAVA_OPTS="${JAVA_OPTS} -Dtmtbl.solver.mem_limit=50"
```


 On Windows:
```
set JAVA_OPTS=%JAVA_OPTS% -Dtmtbl.solver.mem_limit=50
```


 Or by adding the line in Tomcat/conf/catalina.properties
```
tmtbl.solver.mem_limit=50
```


 This limit is megabytes, it is applicable only on the tomcat side, the same limit is used for all solver servers.

## Q8: Error during query: Unexpected Exception: java.io.CharConversionException message given: null


 This problem is discussed in this MySQL forum thread [http://forums.mysql.com/read.php?39,142452,142452](http://forums.mysql.com/read.php?39,142452,142452) where some potential solutions are listed as well.


 In most cases the problem seemed to be resolved by using a newer version of Java (e.g., java 1.5 instead of some 1.4.x).


 Other solution seems to be to set default-character-set variable to utf8 in mysql configuration (usually located at /etc/my.cnf, both mysqld and client sections):
```
[client]
```
```
default-character-set=utf8
```
```
[mysqld]
```
```
default-character-set=utf8
```


 The mysql will use utf8 after it is restarted.

## Q9: Unable to configure hibernate, reason: Connection refused: connect OR No route to host


 Such an exception is thrown when [Hibernate](http://www.hibernate.org) (the tool we us for communicating with the database) is not able to validate the configuration XML files, with the DTD that is available online at [http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd](http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd). Basically, it was unable to download this hibernate-configuration-3.0.dtd file.


 Do you have an internet connection and can you access this url (i.e., [http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd](http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd))?


 If so, try to restart tomcat again. Occasionally it fails to get this file because of some timeout etc.


 If not, there are the following two workarounds:


 1. Disconnect all your networks, then start tomcat, then you can connect them back. If there is no connection, hibernate does not try to validate the given configuration (but it will still load it). Your need to have your database installed on the same machine as the tomcat though.


 2. Remove the following lines from **hibernate.cfg.xml** (2nd – 4th line)
```
<!DOCTYPE hibernate-configuration
```
```
PUBLIC "-//Hibernate/Hibernate Configuration DTD//EN"
```


 ```"```[http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd](http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd)```" >```


 This file is located in the file **timetable.jar**, that is located in **UniTime.war** (in folder WEB-INF/lib). Both files (**UniTime.war**, **timetable.jar**) can unzipped/zipped using ZIP (e.g., WinZip).


 Alternatively, you can go to Tomcat/webapps and:

* Delete UniTime.war (it should be already unzipped into Tomcat/webapps/UniTime)

* Create folder classes under Tomcat/webapps/UniTime/WEB-INF

* Unzip all content of Tomcat/webapps/UniTime/WEB-INF/lib/timetable.jar into the new classes folder (Tomcat/webapps/UniTime/WEB-INF/classes)

* Delete timetable.jar (files from the folder classes will be used instead)

* Edit file classes/hibernate.cfg.xml, delete the above three lines

* Start tomcat

## Q10: ClassNotFoundException: com.mysql.jdbc.Driver


 The "ClassNotFoundException: com.mysql.jdbc.Driver" indicates that the MySQL JDBC driver was not found. You can download the driver from [http://dev.mysql.com/downloads/connector/j/](http://dev.mysql.com/downloads/connector/j/). It needs to be unzipped and placed in the Tomcat's lib folder (something like C:\Program Files\Apache Software Foundation\Tomcat 7.0\lib\ on Windows or /var/lib/tomcat7/lib on Linux). The driver file is named something like mysql-connector-java-5.1.36.jar.


 If putting the driver in Tomcat/lib does not work, you can try to put it in Tomcat/webapps/UniTime/WEB-INF/lib folder instead.


 You will need to restart the Tomcat afterward.
