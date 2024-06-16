---
layout: default
title: Email
---


UniTime is using [Java Mail](http://www.oracle.com/technetwork/java/javamail/index.html) to send emails and it can be configured using the appropriate mail.XXX properties. Additional information can be provided using unitime.email.XXX properties.

Here is an example using Gmail:
```
mail.smtp.host=smtp.gmail.com
mail.smtp.auth=true
mail.smtp.starttls.enable=true
mail.smtp.socketFactory.port=465
mail.smtp.socketFactory.class=javax.net.ssl.SSLSocketFactory
mail.smtp.user=username@gmail.com
mail.smtp.password=XXX
unitime.email.sender=username@gmail.com
unitime.email.sender.name=UniTime Application
unitime.email.replyto=username@gmail.com
unitime.email.replyto.name=UniTime Support
```

These properties can be set on the [Application Configuration](application-configuration) page or using the custom properties file (see [UniTime Installation](installation) for more details). The defaults are set in the [application.properties file](https://github.com/UniTime/unitime/blob/master/JavaSource/application.properties#L93-L132).

There are a few more unitime.email.XXX properties that can be set, see the [Application Configuration](application-configuration) page for more detail.
