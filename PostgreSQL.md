---
layout: default
title: PostgreSQL
---


This document explains how UniTime can be used with PostgreSQL. You can either create a new database (follow step 3A and skip 3B) or migrate an existing MySQL database (follow step 3B instead of 3A).

## 1. Prerequisites

Install PostgreSQL 12.0 (e.g., from [https://www.postgresql.org/download/](https://www.postgresql.org/download/)), using the default port 5432, and a custom password.

Download the JDBC Driver (e.g., from [https://jdbc.postgresql.org/download.html](https://jdbc.postgresql.org/download.html),) and place it under Tomcat/lib.

If migrating from an existing MySQL database, install pgloader. See [https://github.com/dimitri/pgloader](https://github.com/dimitri/pgloader) for instructions.

UniTime needs to be updated to version 4.4.139 or later.

## 2. Create timetable user and timetable database

Using the same name and credentials as the default UniTime database:
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

## 3A. Create database schema and populate it with the initial content (Variant A)

Use [Documentation/Database/PostgreSQL/timetable.sql](https://raw.githubusercontent.com/UniTime/unitime/maint_UniTime44/Documentation/Database/PostgreSQL/timetable.sql) to create the database schema and populate it with initial data.
```
psql -U timetable <timetable.sql
Password: unitime
```

Note: The timetable database will contain the woebegon-example data as the [online demo](https://demo.unitime.org). You can delete the two example sessions once a new session is created (the status needs to be changed to Session Finished first), using the Administration > Academic Sessions > [Academic Sessions](academic-sessions) page.

## 3B. Migrate an existing MySQL database (Variant B)

Create configuration file, e.g., migration.cfg:
```
LOAD DATABASE
  FROM mysql://timetable:unitime@localhost:3306/timetable
  INTO postgresql://timetable:unitime@localhost/timetable
```


```
CAST type int when (= precision 1) to boolean drop typemod using tinyint-to-boolean,
  type decimal when (and (= precision 1) (= scale 0)) to boolean drop typemod using tinyint-to-boolean,
  type decimal when (and (= precision 20) (= scale 0)) to bigint drop typemod,
  type decimal when (and (= precision 22) (= scale 0)) to bigint drop typemod,
  type decimal when (and (= precision 19) (= scale 0)) to bigint drop typemod,
  type decimal when (and (= precision 10) (= scale 0)) to int drop typemod
;
```

Execute pgloader:
```
pgloader -v migration.cfg
```

Note: If you get the MYSQL-UNSUPPORTED-AUTHENTICATION error, make the following changes:

A) Edit my.cnf and in [mysqld] section add the following line (restart MySQL afterward):
```
default-authentication-plugin=mysql_native_password
```

B) Update timetable user password to mysql_native_password (using mysql -uroot -p):
```
alter user timetable@localhost
  identified with mysql_native_password by 'unitime';
```

Once done, run the followings SQLs (using psql -U timetable)
```
alter table distribution_type add temp_seq boolean default false;
update distribution_type set temp_seq = 't' where sequencing_required = '1';
alter table distribution_type drop sequencing_required;
alter table distribution_type rename column temp_seq to sequencing_required;
```

## 4. Update UniTime connection properties

In the UniTime custom properties (see [UniTime Installation](installation), section Customization), replace MySQL connection properties with the following:
```
connection.url=jdbc:postgresql://localhost:5432/timetable
connection.driver_class=org.postgresql.Driver
dialect=org.hibernate.dialect.PostgreSQL9Dialect
connection.username=timetable
connection.password=unitime
default_schema=timetable
hibernate.dbcp.validationQuery=select 1
hibernate.globally_quoted_identifiers=true
```

Start UniTime, check the logs for any errors.
