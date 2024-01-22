---
layout: default
title: LDAP Authentication / Lookup
---


## LDAP Authentication


 Since UniTime 3.4, we use [Spring Security](http://projects.spring.io/spring-security/) to provide authentication and authorization. First of all, the LDAP version of the Spring Security Context (file [springSecurityContextLDAP.xml](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContextLDAP.xml)) must be used instead of the default context (file [springSecurityContext.xml](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContext.xml)). This can be done by setting the following property as Java system variable, e.g., in Tomcat/conf/catalina.properties
```
unitime.spring.context.security=securityContextLDAP.xml
```


 Besides of that, the LDAP server can be configured using the following custom properties. These properties are needed during the UniTime startup, so they need to be added in Tomcat/conf/catalina.properties or in a UniTime custom properties file (setting them using the [Application Configuration](application-configuration) will not do, see [UniTime Installation: Customization](http://help.unitime.org/Timetabling_Installation#TOC-Customization)  for more details).
```
unitime.authentication.ldap.url=ldaps://some.university.edu:636/dc=university,dc=edu
unitime.authentication.ldap.user-dn-pattern=uid={0},ou=authenticate
unitime.authentication.ldap.group-search-base=ou=authorize
unitime.authentication.ldap.group-role-attribute=exid
unitime.authentication.ldap.group-search-filter=uid\={1}
```


 These properties are used directly to setup `<ldap-server>` and `<authentication-manager>` in the [security context](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContext.xml#L100) (see the relevant parts below). See [LDAP Authentication](http://docs.spring.io/spring-security/site/docs/3.1.x/reference/ldap.html) for more details.
```
<ldap-server url="${unitime.authentication.ldap.url}"/>
<authentication-manager>
       <ldap-authentication-provider
                user-dn-pattern="${unitime.authentication.ldap.user-dn-pattern}"
                group-search-base="${unitime.authentication.ldap.group-search-base}"
                group-role-attribute="${unitime.authentication.ldap.group-role-attribute}"
                group-search-filter="${unitime.authentication.ldap.group-search-filter}"
                user-context-mapper-ref="unitimeUserContextMapper"
        />
</authentication-manager>
```


 For more information about the LDAP authentication, please see UniTime [security context](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContext.xml#L100) and the Spring [LDAP Authentication](http://docs.spring.io/spring-security/site/docs/3.1.x/reference/ldap.html) reference manual.

## LDAP Lookup


 LDAP can also be used for people lookup (as one of the sources, besides instructors, staff, students, timetabling managers, and event contacts). To set LDAP lookup, you need to use the following properties:
```
#Ldap for People Lookup
tmtbl.lookup.ldap=ldap://directory.university.edu:389
tmtbl.lookup.ldap.name=ou=directory,dc=university,dc=edu
tmtbl.lookup.ldap.phone=phone,officePhone,homePhone,telephoneNumber
tmtbl.lookup.ldap.department=department
tmtbl.lookup.ldap.position=position,title
```
[](http://www.google.com/url?q=http%3A%2F%2Fsites.google.com%2Fa%2Funitime.org%2Fhelp%2FLDAP%2FScreen%2520shot%25202011-01-28%2520at%25203.40.37%2520PM.png&sa=D&sntz=1&usg=AOvVaw08MmDljOCt6YwvARITrnyz)


 See [PeopleLookupBackend#findPeopleFromLdap](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/server/lookup/PeopleLookupBackend.java#L375) for the implementation.


 Moreover, it is expected that the LDAP lookup only returns usernames (attribute uid, not the actual external ids). If external ids are different from usernames, there is a class ([SpringLdapExternalUidTranslation](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/spring/ldap/SpringLdapExternalUidTranslation.java)) that provides translation between these two.
```
# Translation between LDAP uid and UniTime's external user id
tmtbl.externalUid.translation=org.unitime.timetable.spring.ldap.SpringLdapExternalUidTranslation
unitime.authentication.ldap.uid2ext=uid={0},ou=identify
unitime.authentication.ldap.ext2uid=extid={0},ou=identify
```


 The above one is using the LDAP authentication module to translate usernames (uid attribute) into external ids (extid attribute).

## Timetable Managers / Instructors Validation


 There is also a possibility to use LDAP to validate timetable mangers and instructors.
```
# External user lookup using LDAP
tmtbl.manager.external_id.lookup.class=org.unitime.timetable.spring.ldap.SpringLdapExternalUidLookup
tmtbl.manager.external_id.lookup.enabled=true
tmtbl.instructor.external_id.lookup.class=org.unitime.timetable.spring.ldap.SpringLdapExternalUidLookup
tmtbl.instructor.external_id.lookup.enabled=true
unitime.authentication.ldap.identify=uid={0},ou=identify
```


 If enabled, the interface ([SpringLdapExternalUidLookup](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/spring/ldap/SpringLdapExternalUidLookup.java)) is used to validate (and/or translate) the entered username / external id. The above implementation also uses the LDAP authentication module (with a query provided in the tmtbl.authenticate.ldap.identify property).

## Notes


 Using some LDAP explorer (e.g., JXplorer, [http://jxplorer.org/](http://jxplorer.org/)) may help you to find out all the settings (e.g., what certificates you need, or how the query should look like) in a more interactive way.
