---
layout: default
title: Localization
---


## Language settings


 There is no need to rebuild the application for a particular language. When the application is built, all the messages files in all the available languages are included. The default locale can be changed by setting the application property unitime.locale through the Administration > Defaults > [Configuration](application-configuration) page.
```
unitime.locale=en
```


 For a particular HTTP session, the locale can be also changed using the locale parameter, e.g., see our online demo in Czech: [https://demo.unitime.org/UniTime?locale=cs](https://demo.unitime.org/UniTime?locale=cs).


 It is also possible to tell the application to take the language settings from the browser. This is done in the [LocaleFilter](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/filter/LocaleFilter.java), when the use-browser-settings parameter is set to true (e.g., by [web.xml](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/web.xml#L248))


 At the moment, the following localizations are available in the official UniTime build:

* en ... English (default)
* en_UK ... English, but using 24-hour time format and MM.DD.YYYY dates
* cs ... Czech
* pl ... Polish

## Translating UniTime using POEditor


 Starting with UniTime 4.7, we use [POEditor.com](https://poeditor.com/projects/view?id=568029) to support the cooperation of users on the translation of UniTime to other languages. Please note that if you want your translation to be a part of the standard distribution of UniTime, you need to sign a [contributor license agreement](http://www.unitime.org/uct_license.php) for Apereo.


 If you are interested in translating UniTime into a particular language, please send us your email at [support@unitime.org](mailto:support@unitime.org), and we will give you permission in POEditor. Alternatively, you can request to join the translation of UniTime at [poeditor.com/join/project/Aa5qIUPsnp](https://poeditor.com/join/project/Aa5qIUPsnp) .


 With POEditor.com, messages are translated at [poeditor.com/projects/view?id=568029](https://poeditor.com/projects/view?id=568029) . To test the translation in your version of UniTime, you will need to make a custom build using the following procedure:

#### 1. Have a local clone of the UniTime repository

```
git clone https://github.com/UniTime/unitime.git
cd unitime
```

#### 2. Download the translation for your localization using the 2-letter language code  (e.g., pl for Polish) in the UniTime project

```
ant -Dlocale=pl import-translations
```

This will use Apache Ant to download the latest transactions from poeditor.com and create the appropriate .properties files. It will also make sure that the given language is registered in [UniTime.gwt.xml](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/UniTime.gwt.xml#L31).

#### 3. Make a custom UniTime build

```
ant build
```

Once done, the new build is available in the Distributions folder (e.g., Distributions/UniTime.war), which can be deployed in the same way as the official build.

## Notes


 If you want to help with translation to another language, please consider looking at the English [dictionary](university-timetabling-application-dictionary), which contains terminology used in UniTime in the original English version. It is advisable to start by translating these terms first, then fill in the translation of particular messages.


 If you wish to use a different tool to provide translations (such as [POEdit](https://poedit.net/)), the following command
```
ant -Dlocale=XX export-translations
```


 can be used to export the existing translations of the given XX language into a PO format. The generated PO file is available under Documentation/Translations (e.g., Documentation/Translations/UniTime4.7_XX.po).


 A modified PO file can be imported back by using
```
ant -Dlocale=XX -Ddownload=false import-translations
```


 where XX is the 2-letter language code, and the translations are imported from the Documentation/Translations/UniTime4.7_XX.po file.

## Implementation Details


 Most of the UniTime application was written using [Apache Struts](http://struts.apache.org/), however, new pages and components are written using [Google Web Toolkit](http://code.google.com/webtoolkit/) (GWT). For localization of GWT parts, we use its [i18n](http://code.google.com/webtoolkit/doc/latest/tutorial/i18n.html) capabilities.


 In short, all text messages are put into a Messages interface (e.g., see [StudentSectioningMessages](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/resources/StudentSectioningMessages.java)), which is then used by calling these methods on a class created calling GWT.create(message interface), e.g., see [this widget](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/client/sectioning/StudentSectioningWidget.java). Note that this only works in the client code (the code that gets compiled into JavaScript); however, for the server side, we have created a very similar approach so that the created Messages interfaces can be reused as we move more towards GWT in the future. We use this technique for both the server side of the GWT-based pages and components as well as for the old Struts-based pages and JSPs. For server-side Java code (e.g., Struts forms and actions), the only difference is that the Messages class is instantiated using the [Localization](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/localization/impl/Localization.java) class. In Java Server Pages (JSP) files, we have two tags <loc:bundle/> and <loc:message/> that are providing the localized strings (e.g., see [here](https://github.com/UniTime/unitime/blob/master/WebContent/user/classEdit.jsp#L118), the tags are defined [here](https://github.com/UniTime/unitime/blob/master/WebContent/WEB-INF/tld/localization.tld)).


 An example of using localization tags in a JSP file:
```
<%@ taglib uri="/WEB-INF/tld/localization.tld" prefix="loc" %>
<loc:bundle name="CourseMessages">

  <%-- translated message, using loc:message, e.g.,
       titleRemoveRoomPreferences=Remove Room Preferences
    -->
<loc:message name="titleRemoveRoomPreference"/>

  <%-- translated message with one argument, e.g.,
       labelConfiguration=Configuration {0})
    -->
  <loc:message name="labelConfiguration"><bean:write property='configName'/></loc:message>

  <%-- translated message, using MSG property -->
  <%=MSG.confirmRoomSizeDifferentFromCapacity()%>

  <%-- additional message bundle -->
  <loc:bundle name="ConstantsMessages" id="CONST">
    <loc:messsage name="monday" id="CONST"/>
    <%=MSG.sunday()%>
  </loc:bundle>
</loc:bundle>
```


 An example of using localization in a Java file:
```
protected final static CourseMessages MSG = Localization.create(CourseMessages.class);
...
// Throw a localized exception if the user is not logged in
if (!Web.isLoggedIn(request.getSession()))
 throw new Exception(MSG.exceptionAccessDenied());

// Localized message
MSG.listInstructors(department.getDeptCode(), department.getName())
```


 An example of using localization in a GWT client code:
```
public static final StudentSectioningMessages MESSAGES =
                         GWT.create(StudentSectioningMessages.class);

// Localized button
// buttonRequests=<u>R</u>equests
iRequests = new Button(MESSAGES.buttonRequests());

// Localized message with multiple arguments
// backToBackDistance=Distance to travel from {0} is approx. {1} minutes. 
MESSAGES.backToBackDistance(clazz.getBackToBackRoom(), clazz.getBackToBackDistance()
```

 [Here](https://github.com/UniTime/unitime/commit/ffb47dd70f2df752f45f7c2170da6b0f3b7633c2) is an example of a change localizing a particular page. The default messages are in English, the language-dependent messages are in a property file with the same name (plus identification of the language using two character iso language code), e.g., see [Czech translation](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/localization/messages/CourseMessages_cs.properties) of [CourseMessages](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/localization/messages/CourseMessages.java).


 Struts localization files are available in [org.unitime.localization.messages](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/localization/messages) package, GWT localization files in [org.unitime.timetable.gwt.resources](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/#unitime%2Ftimetable%2Fgwt%2Fresources) package.


 Note that the language has to be added in the [UniTime.gwt.xml](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/UniTime.gwt.xml#L31) (as a supported language, extending locale property) for the GWT compiler to create the appropriate language mutation.
