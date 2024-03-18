---
layout: default
title: OAuth2 Authentication
---

## OAuth2 Spring Security Context

Since UniTime 4.8, it is possible to enable OAuth2 authentication in UniTime.

First of all, the OAuth2 version of the Spring Security Context (file [springSecurityContextOAuth2.xml](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/securityContextOAuth2.xml)) must be used instead of the default context. This can be done by setting the following property as Java system variable, e.g., in `Tomcat/conf/catalina.properties`
```
unitime.spring.context.security=securityContextOAuth2.xml
```

**Important:** Please note that the above property cannot be set in the UniTime's custom properties because it says which security context configuration XML file is to be loaded in and setting the property in the UniTime's custom properties is too late.

## OAuth2 Configuration

The following custom properties need to be set. These properties are needed during the UniTime startup, so they need to be added in Tomcat/conf/catalina.properties or in a UniTime custom properties file (setting them using the [Application Configuration](application-configuration) will not do, see [UniTime Installation: Customization](installation#customization)  for more details).

Goolge, Facebook, Okta, GitHub, and Azure should work out of the box. See the following two examples for Google and Azure Active Directory. Additional services can be added in the [UniTimeOAuth2ClientRegistrationRepository](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/spring/oauth2/UniTimeOAuth2ClientRegistrationRepository.java) class.

### Using Google
```
# OAuth2 Authentication Provider
# Available values: google, facebook, github, okta, or azure
unitime.authentication.oauth2.provider=google
# Client id and secret from the registration (e.g., using Google Developper Console)
# See https://developers.google.com/identity/protocols/oauth2/web-server for more details
unitime.authentication.oauth2.client-id=FIXME
unitime.authentication.oauth2.client-secret=FIXME
# Authentication scope
unitime.authentication.oauth2.scope=email,profile
# Attribute containing user's name
unitime.authentication.oauth2.name-attribute=name
# Attribute containing user's external unique id
unitime.authentication.oauth2.id-attribute=email
# Optional: translation of the provided external id (see tmtbl.externalUid.translation)
unitime.authentication.oauth2.id-translate=false
# Optional: trim leading zeros from the user external id
unitime.authentication.oauth2.id-trim=false
# Login page OAuth2 authentication message
unitime.authentication.oauth2.login-message=Log in using Google.
# UniTime address, needed to corretly formulate the authentication redirect URL
unitime.url=https://demo.unitime.org/UniTime
```

The OAuth2 login will be available by clicking the ***Log in using Google.*** link on the Login page.
Alternatively, the Google login page can be used to replace the UniTime's default login page (only allowing Google authentication)
```
tmtbl.login_url=oauth2/authorization/google
tmtbl.login_method=redirect
unitime.authentication.oauth2.logout=/main.action?op=logout
```

Please note that the return URL, such as `https://demo.unitime.org/UniTime/login/oauth2/code/google`, must be registered in the Google Developper Console. See the Google's [Using OAuth 2.0 for Web Server Application](https://developers.google.com/identity/protocols/oauth2/web-server) for more details.

### Using Azure Active Directory
```
# OAuth2 Authentication Provider
# Available values: google, facebook, github, okta, or azure
unitime.authentication.oauth2.provider=azure
# Tenant id, client id and secret from the Azure Active Directory configuration
unitime.authentication.oauth2.client-id=FIXME
unitime.authentication.oauth2.client-secret=FIXME
unitime.authentication.oauth2.tenant-id=FIXME
# Authentication scope
unitime.authentication.oauth2.scope=openid,email,profile
# Attribute containing user's name
unitime.authentication.oauth2.name-attribute=name
# Attribute containing user's external unique id
unitime.authentication.oauth2.id-attribute=email
# Optional: translation of the provided external id (see tmtbl.externalUid.translation)
unitime.authentication.oauth2.id-translate=false
# Optional: trim leading zeros from the user external id
unitime.authentication.oauth2.id-trim=false
# Login page OAuth2 authentication message
unitime.authentication.oauth2.login-message=Log in using Azure AD.
# UniTime address, needed to corretly formulate the authentication redirect URL
unitime.url=https://demo.unitime.org/UniTime
```

The OAuth2 login will be available by clicking the ***Log in using Azure AD.*** link on the Login page.
Alternatively, the Azure AD login page can be used to replace the UniTime's default login page (only allowing Google authentication)
```
tmtbl.login_url=oauth2/authorization/azure
tmtbl.login_method=redirect
unitime.authentication.oauth2.logout=/main.action?op=logout
```

If the external id is in an additional parameter, such as `onPremisesSamAccountName`, an additional call to Microsoft Graph API can be added.
```
# Query Graph API for onPremisesSamAccountName
unitime.authentication.oauth2.queryAttributes=https://graph.microsoft.com/v1.0/me?$select=onPremisesSamAccountName
# Attribute containing user's external unique id
unitime.authentication.oauth2.id-attribute=onPremisesSamAccountName
```

Please note that the return URL, such as `https://demo.unitime.org/UniTime/login/oauth2/code/azure`, must be registered in the Azure Active Directory configuration. See the [Quickstart: Register an application with the Microsoft identity platform](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app) for more details.

## Mapping user names to external ids

By default, the OAuth2 user name must match the external id of the user in UniTime for the authenticated user to be successfully associated with the appropriate user roles in UniTime (Timetable Manager, Instructor, Student). It is also possible to pick up a custom attribute containing user's external id and full name.
```
unitime.authentication.oauth2.id-attribute=extid
unitime.authentication.oauth2.name-attribute=fullname
unitime.authentication.oauth2.id-trim=false
```

The above properties contain name of the attribute containing the user's external id (should match the external id of the appropriate student, instructor, or timetable manager) and user's name (optional). The last parameter, if set true, can be used to enable trimming of leading zeroes of the external id.

If OAuth2 does not return external id of the user, a translation class can be plugged in. The following example is using an SQL command to translate user name to external id and back.
```
unitime.authentication.oauth2.id-translate=true
tmtbl.externalUid.translation=org.unitime.timetable.spring.security.CustomSQLExternalUidTranslation
unitime.custom.sql.uid2ext=select external_uid from %SCHEMA%.users where username = ?
unitime.custom.sql.ext2uid=select username from %SCHEMA%.users where external_uid = ?
```

The first property enabled id translation (it can be used with or without the id-attribute parameter). The second parameter provides the translation class (any class implementing the [ExternalUidTranslation](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/interfaces/ExternalUidTranslation.java) interface capable of translating ids from LDAP type (username) to User type (external id) and back), using the [CustomSQLExternalUidTranslation](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/spring/security/CustomSQLExternalUidTranslation.java) class. This class is using SQL commands that can translate user name to external id (third parameter) and external id to user name (fourth parameter). In these queries, %SCHEMA% is replaced by the schema containing UniTime database (property default_schema, defaults to timetable) and ? is the given user name / external id.
