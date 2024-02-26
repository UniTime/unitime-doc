---
layout: manual
title: Migrating to PostgreSQL
version: 4.4.139
updated: November, 2019
---

### Table of Contents
{:.no_toc}
* table
{:toc}


 

## Migration Steps

1. Update UniTime to version 4.4.139 or later
2. Install PostgreSQL 12.0 from [https://www.postgresql.org/download/](https://www.postgresql.org/download)

    (using the default port 5432, and a custom password)

    Or using apt-get (Brew/MacPorts on Mac)
3. Install pgloader (using pgloader, [https://github.com/dimitri/pgloader](https://github.com/dimitri/pgloader))

    Installation for Mac:

    ```
    /usr/bin/ruby -e \
    "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    brew install --HEAD pgloader
    ```

    On Linux, it should be sufficient to do `apt-get install pgloader`

4. Create timetable user and timetable database

    Using the same name and credentials as the default UniTime database:

    `createuser --interactive --pwprompt -U postgres`

    ```
    Enter name of role to add: timetable
    Enter password for new role: unitime
    Enter it again: unitime
    Shall the new role be a superuser? (y/n) n
    Shall the new role be allowed to create databases? (y/n) y
    Shall the new role be allowed to create more new roles? (y/n) n
    Password: <password provided during install>
    ```
 
    `createdb timetable -U timetable -O timetable`

    ```
    Password: unitime
    ```

5. Migrate MySQL database (including tables, indexes, and content)

    Create configuration file, e.g., migration.cfg:
    ```
    LOAD DATABASE
      FROM mysql://timetable:unitime@localhost:3306/timetable
      INTO postgresql://timetable:unitime@localhost/timetable

    CAST type int when (= precision 1) to boolean drop typemod using tinyint-to-boolean,
      type decimal when (and (= precision 1) (= scale 0)) to boolean drop typemod using tinyint-to-boolean,
      type decimal when (and (= precision 20) (= scale 0)) to bigint drop typemod,
      type decimal when (and (= precision 22) (= scale 0)) to bigint drop typemod,
      type decimal when (and (= precision 19) (= scale 0)) to bigint drop typemod,
      type decimal when (and (= precision 10) (= scale 0)) to int drop typemod
    ;
    ```

    Execute pgloader:
    `pgloader -v migration.cfg`


    **Note:** The first time I tried, I was getting MYSQL-UNSUPPORTED-AUTHENTICATION error back. Making the following changes did the trick:

    1. Edit my.cnf and in [mysqld] section add the following line (restart MySQL afterward):

        ```
        default-authentication-plugin=mysql_native_password
        ```
    
    2. Update timetable user password to mysql_native_password (using `mysql -uroot -p`):

        ```
        alter user timetable@localhost

        identified with mysql_native_password by 'unitime';
        ```


6. Run the followings SQLs (using `psql -U timetable`)

    ```
    alter table distribution_type add temp_seq boolean default false;
    update distribution_type set temp_seq = 't' where sequencing_required = '1';
    alter table distribution_type drop sequencing_required;
    alter table distribution_type rename column temp_seq to sequencing_required;
    ```

7. Install JDBC Driver downloaded from [https://jdbc.postgresql.org/download.html](https://jdbc.postgresql.org/download.html)

    Placed under Tomcat/lib (where the mysql JDBC driver is located now)

8. Change UniTime connection properties

    Replace MySQL connection properties with the following:
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
 
9. Start UniTime, check the logs for any errors.

## Potential Issues

* Booleans do not match with numbers (1) -- e.g., CourseOffering.isControl = 1 is wrong

* Strings do not match with numbers -- e.g., CourseOfferings.uniqueId = '1234' is wrong

* Column names must be escaped (e.g., offset is a reserved word), in which case they need to be all in lowercase (comparison is case sensitive)

* Bit operations do work on integers but not on numeric types

* Custom types for XMLs do not work, but we only have a few cases where these are used and these can be easily replaced (already done in commit [9ed26f6](https://github.com/UniTime/unitime/commit/9ed26f6b2381aa8b8678b781161336e562442b57))

* A query using distinct cannot have order by (select distinct s from Student s… order by s.lastName)

* Sequences can be used (as they are when we use Oracle), but setting up these (instead of the table Hi/Lo we use for MySQL) will mean extra work (can be done, if desired)


 
