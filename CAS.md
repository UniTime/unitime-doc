---
layout: default
title: CAS Authentication
---


## Prerequisites

There are two prerequisites that usually need to be done before CAS authentication can be enabled in UniTime.

* UniTime has to be accessed through https (not http). This can be done either by enabling SSL directly in Tomcat (see [SSL Configuration HOW-TO](http://tomcat.apache.org/tomcat-7.0-doc/ssl-howto.html) for more details) or by proxying UniTime through SSL enabled Apache web server (see [AJP Connector](https://tomcat.apache.org/tomcat-7.0-doc/config/ajp.html) and [Proxy Support HOW TO](https://tomcat.apache.org/tomcat-7.0-doc/proxy-howto.html) for more details).

* The CAS server can be accessed from UniTime's URL (see unitime.url property bellow)

## CAS Spring Security Context

Since UniTime 3.5, it is possible to enable CAS authentication in UniTime. First of all, the CAS version of the Spring Security Context (file [springSecurityContextCAS.xml](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContextCAS.xml)) must be used instead of the default context (file [springSecurityContext.xml](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContext.xml)). This can be done by setting the following property as Java system variable, e.g., in Tomcat/conf/catalina.properties
```
unitime.spring.context.security=securityContextCAS.xml
```

Please note that the above property cannot be set in the UniTime's custom properties because it says which security context configuration XML file is to be loaded in and setting the property in the UniTime's custom properties is too late.

## CAS Configuration

The following custom properties need to be set. These properties are needed during the UniTime startup, so they need to be added in Tomcat/conf/catalina.properties or in a UniTime custom properties file (setting them using the [Application Configuration](application-configuration) will not do, see [UniTime Installation: Customization](installation#customization)  for more details).
```
tmtbl.login_url=selectPrimaryRole.action
tmtbl.login_method=redirect
unitime.cas.url=https://www.university.edu/apps/account/cas
unitime.url=https://demo.unitime.org/UniTime
```

The first two properties are needed to ensure that authentication does not go through the UniTime's default login page. The unitime.cas.url property points to the address of the CAS server and unitime.url points to the address of UniTime. This address is passed to the CAS server (it must be enabled on the CAS side) and the control is returned back to this URL when the user is successfully authenticated.

## Mapping user names to external ids

By default, the CAS user name must match the external id of the user in UniTime for the authenticated user to be successfully associated with the appropriate user roles in UniTime (Timetable Manager, Instructor, Student). It is also possible to pick up a custom CAS attribute containing user's external id and full name.
```
unitime.authentication.cas.id-attribute=extid
unitime.authentication.cas.name-attribute=fullname
unitime.authentication.cas.id-trim=false
```

The above properties contain name of the attribute containing the user's external id (should match the external id of the appropriate student, instructor, or timetable manager) and user's name (optional). The last parameter, if set true, can be used to enable trimming of leading zeroes of the external id.

If CAS does not return external id of the user, a translation class can be plugged in. The following example is using an SQL command to translate user name to external id and back.
```
unitime.authentication.cas.id-translate=true
tmtbl.externalUid.translation=org.unitime.timetable.spring.security.CustomSQLExternalUidTranslation
unitime.custom.sql.uid2ext=select external_uid from %SCHEMA%.users where username = ?
unitime.custom.sql.ext2uid=select username from %SCHEMA%.users where external_uid = ?
```

The first property enabled id translation (it can be used with or without the id-attribute parameter). The second parameter provides the translation class (any class implementing the [ExternalUidTranslation](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/interfaces/ExternalUidTranslation.java) interface capable of translating ids from LDAP type (username) to User type (external id) and back), using the [CustomSQLExternalUidTranslation](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/spring/security/CustomSQLExternalUidTranslation.java) class. This class is using SQL commands that can translate user name to external id (third parameter) and external id to user name (fourth parameter). In these queries, %SCHEMA% is replaced by the schema containing UniTime database (property default_schema, defaults to timetable) and ? is the given user name / external id.

## Logout URL

When the user clicks the Logout menu item, by default he/she is only logged out of UniTime, with the option to log out of CAS on the second click.

You have been successfully logged out of UniTime, click __here__ to log out of all other applications as well.

If it is desired to log the user out of CAS right away, the following property needs to be set as follows:
```
unitime.cas.logout=/logout
```

When the above property is set as such, the user is logged out of CAS server once he/she clicks the Logut item in UniTime.

## More details

For more details about the CAS authentication, see

* CAS version of the Spring Security Context, file [springSecurityContextCAS.xml](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContextCAS.xml)

* [UniTimeAuthenticationUserDetailsService](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/spring/security/UniTimeAuthenticationUserDetailsService.java) (class responsible for getting UniTime user's details from the CAS authentication token)

* [Spring Security: CAS Authentication Manual](https://docs.spring.io/spring-security/site/docs/3.1.x/reference/cas.html)

* [CAS User Manual](http://jasig.github.io/cas/4.1.x/index.html) ([older version](https://wiki.jasig.org/display/CASUM/Home))
