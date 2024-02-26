---
layout: manual
title: UniTime Configuration for Student Scheduling Only
version: 4.X
updated: January, 2020
---

### Table of Contents
{:.no_toc}
* table
{:toc}

UniTime Configuration for Student Scheduling Only


The purpose of the document is to describe how to configure UniTime for student scheduling using a class schedule imported from Banner rather than using UniTime to build a timetable.  This document describes the basic data that needs to be imported into the UniTime system and how to configure Banner XE Registration integration.  This document does not cover running the batch student scheduling process or real time student scheduling.

# UniTime Installation


The first step in using UniTime for student scheduling is to have a working instance of the UniTime system. Instructions for installing the UniTime system can be found at: [https://help.unitime.org/installation](../installation).


 

# Academic Session Setup


In order to configure UniTime to do student scheduling without first building the course timetable in UniTime, an academic session must be set up along with buildings and rooms. The externally generated course timetable must also be imported. These steps may all be accomplished via XML imports.  The formats required for the XML imports and exports supported by UniTime are defined at [https://www.unitime.org/uct_interfaces.php](https://www.unitime.org/uct_interfaces.php).  The three imports needed to load the required data are the ‘Academic session setup’ import, the ‘Buildings and Rooms’ import and the ‘Courses’ import.  An example of the ‘Academic session setup’ import can be found in [Appendix A](#appendix-a)  An example of the ‘Buildings and Rooms’ import can be found in [Appendix B](#appendix-b).  Please note that there is a trick to using the ‘Buildings and Rooms’ import.  Once the file has been imported, go to the Administration -> Academic Sessions -> Buildings page and press the ‘Update Data’ button or the imported building and room data will not be usable. An example of the ‘Courses’ import can be found in [Appendix C](#appendix-c).


 


For purpose of importing a timetable from Banner the following should be done:

* Set a default date pattern in UniTime that defines the basic full term dates.  Beyond that, date patterns will be created as needed when importing a course timetable.

* The ‘Exact Time’ time pattern will be used for the times of the imported classes.  This time pattern will need to be added to the system.  It is possible to use the one in the sample academic session import xml, or the Administration ->Academic Sessions -> Time Patterns page can be used to configure the time pattern.

* On the class element, the id must be the CRN.

* On the class element, the suffix should be the CRN-Section Number.

* For the config element, the name can just be a 1-up number.

* Treat cross listed courses as separate courses. 

* If a section has multiple meetings of different lengths, or that start at different times, they should have a configuration that has subpart elements with the same “type” fully nested under each other with a suffix defined. The classes should mirror this same nesting.  See attached example in [Appendix C](#appendix-c) for course ENGL 10800.


 


Once the session has been set up and the course timetable loaded, the academic session should be set to the ‘Timetable Published’ status. After this is done the student course requests must be either entered via the Course Requests page or imported.  The ‘Student Course Requests’ xml import can be used to import the data.  [Appendix D](#appendix-d) contains a sample course request xml (please note that course examples used in the sample course request xml do not match up with example courses in the sample timetable).  For more information about the data in the course requests, look at the help page associated with the Course Requests page as the data in the course request portion of the XML mirrors the data entered by the students on that page.  The following link is to this help page:  [http://help.unitime.org/student-course-requests](../student-course-requests).

# Banner XE Registration Integration


To use UniTime integrated into the Banner XE Registration API, the appropriate UniTime configuration properties must be set.  The following table lists the properties that need to be configured and either the value the property should be set to or a description of what the value should be. These can be configured via the Administration -> Defaults -> Configuration page.


 
| Property | Value or description of value | More about the value |
| banner.xe.site | URL of the Banner XE Registration API |  |
| banner.xe.user | Username to use for API if registering as the student, e.g. BAN_STU_API | This does not allow overrides to be used. |
| banner.xe.password | Password for the user |  |
| banner.xe.admin | TRUE | Enable admin feature (systemIn=SB) for users with StudentSchedulingAdvisor permission. |
| banner.xe.admin.user | User name to use for the API when registering the student as an administrator, e.g. BAN_UNITIMEADMIN_API | This allows overrides to be used. |
| banner.xe.admin.password | Password for the user |  |
| banner.xe.adminParameter | systemIn | Use the systemln value. |
| banner.xe.checkMaxHours | TRUE | If you want UniTime to validate the student schedule has not exceeded the max hours for a student set this to TRUE otherwise set it to FALSE. |
| banner.xe.conditionalAddDrop | HAS_DROP | Use this to ensure that when a student schedule change includes a drop that the schedule change will not happen if any part of the change fails.  This prevents the student from being dropped from a course and failing to get into another one. |
| banner.xe.errorWhenNoChange | TRUE | This should be TRUE |
| banner.xe.maxHoursDefault | 99 | If UniTime is checking set this to the max credit hours number, probably around 18 or 20. |
| banner.xe.messages.maxHours | Maximum of {max} credit hours exceeded. | Message to display if the student exceed the max credits. |
| banner.xe.recheck | (Your PIN is invalid\|You have no Registration Time Ticket for the current time\.) | This is a regular expression. If the banner error(s) match this property, the Submit Schedule is available to the student and the eligibility is re-checked when clicked. |
| banner.xe.waitlist | FALSE | This should be FALSE. |
 


 


In addition, go to the Administration -> Solver -> Parameters page and add the parameters in Figures 1 and 2.  The ‘Save.XE.Action.Add’ and other parameters in Figure 1 need to be added to the ‘StudentSctBasic’ group.


 


![UniTime Configuration for Student Scheduling Only](images/student-scheduling-configuration-1.png){:class='screenshot'}
Figure 1


 


 


The ‘Save.XE.NRSaveThreads’ parameter in Figure 2 needs to be added to the ‘StudentSct’ group.   The full default value for the ‘General Database Saver’ parameter is ‘org.unitime.timetable.onlinesectioning.custom.purdue.XEBatchSolverSaver’.


 


![UniTime Configuration for Student Scheduling Only](images/student-scheduling-configuration-2.png){:class='screenshot'}
Figure 2

# Matching UniTime Sessions to Banner Terms

In order for UniTime to use the correct Banner Term information in its exchange of data with Banner, a mapping between the UniTime Academic Session and the Banner Term Code needs to occur.  The [ExternalTermProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/ExternalTermProvider.java) interface that is used to calculate this value. It is plugged in using the unitime.custom.ExternalTermProvider application property.

The default implementation is [org.unitime.timetable.onlinesectioning.custom.purdue.BannerTermProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/purdue/BannerTermProvider.java).  This implementation determines the Banner Term Code via a simple calculation.  For example, if the term starts with Fa, it adds 1 to the year and appends 10 to the end so for an academic session.  With academic year 2019 and academic term Fall the result is 202010.  If the term starts with Spr it append 20 to the year so for an academic session with academic year 2019 and academic term Spring the result is 201920.

If this simple calculation is not sufficient, then the UniTime Banner Add On can be used.  This requires doing a special build of UniTime that incorporates the UniTime Banner Add On.  The UniTime Banner Add On adds tables into UniTime that specifically support integrating Unitime with Banner.  When the Banner Add-On is used, the [org.unitime.banner.onlinesectioning.BannerTermProvider](https://github.com/UniTime/unitime-addons/blob/master/BannerAddOn/JavaSource/org/unitime/banner/onlinesectioning/BannerTermProvider.java) is used to override the default implementation. This implementation adds a BannerSession lookup into a table that specifically maps UniTime Academic Sessions to Banner Term Codes. The implementation falls back to the calculation when the Banner Term Code lookup fails.


The following link contains documentation on how to build UniTime with the UniTime Banner Add On integration: [https://help.unitime.org/manuals/banner-addon-instructions](banner-addon-instructions)


 


Since this documentation is based on a use case in which UniTime is not used to create a course timetable and synchronize it back to Banner, when configuring a Banner session in UniTime, the checkboxes “Store Data for Banner” and “Send Data to Banner” should never be checked.  If it is decided to have a back channel flow of student registrations from Banner into UniTime in addition to the XE Registration API, the queue processor should be configured.  If there are questions about implementing a back channel flow of student registrations from Banner into UniTime, please contact [services@unitime.org](mailto:services@unitime.org) and this process can be discussed.


 


Once the UniTime Banner Add On implementation is in place, it is important to configure using the external term provider via the Administration -> Defaults -> Configuration page.


The “unitime.custom.ExternalTermProvider” property should be set to “org.unitime.banner.onlinesectioning.BannerTermProvider”.


 


This covers the basics of what is necessary to set up an instance of UniTime to batch schedule students.


 


default implementation of calculating the academic session will work for your institution, then you do not need to do anything.  If it does not, then you will need to use the Banner add on.  I can provide information on how to compile and install the add on if it is needed.


 


 



 

# Appendix A

```
<?xml version="1.0" encoding="UTF-8"?>

<sessionSetup term="Fall" year="2019" campus="WL" dateFormat="yyyy/M/d" created="Mon Dec 10 11:42:07 EST 2018">
  <session startDate="2019/8/19" endDate="2019/12/14" classEndDate="2019/12/7" examStartDate="2019/12/9" eventStartDate="2019/8/12" eventEndDate="2019/12/31">
	<holidays>
  	<holiday date="2019/9/2"/>
  	<break startDate="2019/10/7" endDate="2019/10/8"/>
  	<holiday date="2019/11/28"/>
  	<break startDate="2019/11/27" endDate="2019/11/27"/>
  	<holiday date="2019/11/29"/>
  	<break startDate="2019/11/30" endDate="2019/12/1"/>
  	<holiday date="2019/12/24"/>
  	<holiday date="2019/12/25"/>
  	<holiday date="2019/12/26"/>
	</holidays>
  </session>
  <departments>
	<department code="CTRL" externalId="CTRL" name="Central"/>
  </departments>
  <subjectAreas>
	<subjectArea abbreviation="BIOL" title="Biological Sciences" externalId="BIOL" department="CTRL"/>
	<subjectArea abbreviation="CHM" title="Chemistry" externalId="CHM" department="CTRL"/>
	<subjectArea abbreviation="EDCI" title="Educ-Curric &amp; Instruction" externalId="EDCI" department="CTRL"/>
	<subjectArea abbreviation="ENGL" title="English" externalId="ENGL" department="CTRL"/>
	<subjectArea abbreviation="HIST" title="History" externalId="HIST" department="CTRL"/>
	<subjectArea abbreviation="MA" title="Mathematics" externalId="MA" department="CTRL"/>
	<subjectArea abbreviation="MSL" title="Military Science &amp; Leadership" externalId="MSL" department="CTRL"/>
	<subjectArea abbreviation="PHIL" title="Philosophy" externalId="PHIL" department="CTRL"/>
	<subjectArea abbreviation="SOC" title="Sociology" externalId="SOC" department="CTRL"/>
	<subjectArea abbreviation="STAT" title="Statistics" externalId="STAT" department="CTRL"/>
	<subjectArea abbreviation="THTR" title="Theatre" externalId="THTR" department="CTRL"/>
  </subjectAreas>
  <datePatterns>
	<datePattern name="Full Term" type="Standard" visible="true" default="true">
  	<dates fromDate="2019/8/19" toDate="2019/9/1"/>
  	<dates fromDate="2019/9/3" toDate="2019/10/6"/>
  	<dates fromDate="2019/10/9" toDate="2019/11/26"/>
  	<dates fromDate="2019/12/2" toDate="2019/12/7"/>
	</datePattern>
   </datePatterns>
  <timePatterns>
	<timePattern name="Exact Time" nbrMeetings="0" minsPerMeeting="0" type="Exact Time" visible="true" nbrSlotsPerMeeting="0" breakTime="0">
  	<department code="1514"/>
	</timePattern>
  </timePatterns>
  <academicAreas>
	<academicArea externalId="EU" abbreviation="EU" title="Education"/>
	<academicArea externalId="LA" abbreviation="LA" title="Liberal Arts"/>
	<academicArea externalId="M" abbreviation="M" title="Management"/>
	<academicArea externalId="S" abbreviation="S" title="Science"/>
	<academicArea abbreviation="T" title="Technology"/>
	<academicArea externalId="US" abbreviation="US" title="Exploratory Studies"/>
  </academicAreas>
  <academicClassifications>
	<academicClassification externalId="01" code="01" name="01"/>
	<academicClassification externalId="02" code="02" name="02"/>
	<academicClassification externalId="03" code="03" name="03"/>
	<academicClassification externalId="04" code="04" name="04"/>
	<academicClassification externalId="05" code="05" name="05"/>
	<academicClassification externalId="06" code="06" name="06"/>
	<academicClassification externalId="07" code="07" name="07"/>
	<academicClassification externalId="08" code="08" name="08"/>
	<academicClassification externalId="GR" code="GR" name="GR"/>
	<academicClassification code="GR Yr 1" name="Grad Year 1"/>
	<academicClassification code="GR Yr 2" name="Grad Year 2"/>
	<academicClassification externalId="P1" code="P1" name="P1"/>
	<academicClassification code="P2" name="P2"/>
	<academicClassification code="P3" name="P3"/>
	<academicClassification code="P4" name="P4"/>
  </academicClassifications>
  <posMajors>
	<posMajor code="WOST" academicArea="LA" externalId="WOST" name="WOST"/>
	<posMajor code="LING" academicArea="LA" externalId="LING" name="LING"/>
	<posMajor code="COMS" academicArea="LA" externalId="COMS" name="COMS"/>
	<posMajor code="CLCS" academicArea="LA" externalId="CLCS" name="CLCS"/>
	<posMajor code="RUSS" academicArea="LA" externalId="RUSS" name="RUSS"/>
	<posMajor code="SOC" academicArea="LA" externalId="SOC" name="SOC"/>
	<posMajor code="PSY" academicArea="LA" externalId="PSY" name="PSY"/>
	<posMajor code="PRPS" academicArea="LA" externalId="PRPS" name="PRPS"/>
	<posMajor code="ENGL" academicArea="LA" externalId="ENGL" name="ENGL"/>
	<posMajor code="COMP" academicArea="LA" externalId="COMP" name="COMP"/>
	<posMajor code="AMST" academicArea="LA" externalId="AMST" name="AMST"/>
	<posMajor code="PHIL" academicArea="LA" externalId="PHIL" name="PHIL"/>
	<posMajor code="SPNS" academicArea="LA" externalId="SPNS" name="SPNS"/>
	<posMajor code="RELG" academicArea="LA" externalId="RELG" name="RELG"/>
	<posMajor code="POL" academicArea="LA" externalId="POL" name="POL"/>
	<posMajor code="HIST" academicArea="LA" externalId="HIST" name="HIST"/>
	<posMajor code="GRMN" academicArea="LA" externalId="GRMN" name="GRMN"/>
	<posMajor code="CMGN" academicArea="LA" externalId="CMGN" name="CMGN"/>
	<posMajor code="PCOM" academicArea="LA" externalId="PCOM" name="PCOM"/>
	<posMajor code="FACO" academicArea="LA" externalId="FACO" name="FACO"/>
	<posMajor code="MRKT" academicArea="M" externalId="MRKT" name="MRKT"/>
	<posMajor code="ECON" academicArea="M" externalId="ECON" name="ECON"/>
	<posMajor code="MGMT" academicArea="M" externalId="MGMT" name="MGMT"/>
	<posMajor code="ADVA" academicArea="M" externalId="ADVA" name="ADVA"/>
	<posMajor code="ENTR" academicArea="M" externalId="ENTR" name="ENTR"/>
	<posMajor code="FINC" academicArea="M" externalId="FINC" name="FINC"/>
	<posMajor code="ACCT" academicArea="M" externalId="ACCT" name="ACCT"/>
	<posMajor code="CHEM" academicArea="S" externalId="CHEM" name="CHEM"/>
	<posMajor code="BIOH" academicArea="S" externalId="BIOH" name="BIOH"/>
	<posMajor code="BIOL" academicArea="S" externalId="BIOL" name="BIOL"/>
	<posMajor code="CS" academicArea="S" externalId="CS" name="CS"/>
	<posMajor code="PHYS" academicArea="S" externalId="PHYS" name="PHYS"/>
	<posMajor code="MATH" academicArea="S" externalId="MATH" name="MATH"/>
	<posMajor code="IT" academicArea="T" externalId="IT" name="IT"/>
	<posMajor code="ECET" academicArea="T" externalId="ECET" name="ECET"/>
	<posMajor code="CNIT" academicArea="T" externalId="CNIT" name="CNIT"/>
	<posMajor code="ENGT" academicArea="T" externalId="ENGT" name="ENGT"/>
	<posMajor code="MFET" academicArea="T" externalId="MFET" name="MFET"/>
	<posMajor code="AVFT" academicArea="T" externalId="AVFT" name="AVFT"/>
	<posMajor code="PT" academicArea="T" externalId="PT" name="PT"/>
	<posMajor code="UNEX" academicArea="US" externalId="UNEX" name="UNEX"/>
	<posMajor code="UNDV" academicArea="US" externalId="UNDV" name="UNDV"/>
  </posMajors>
  <posMinors/>
  <studentGroups/>
  <studentAccomodations/>
</sessionSetup>
```

# Appendix B

```
<buildingsRooms campus="WL" term="Fall" year="2019">
<building externalId="WALC" abbreviation="WALC" locationX="40.427673" locationY="-86.913216" name="Wilmeth Active Learning Center">
<room externalId="94436" locationX="40.427673" locationY="-86.913216" roomNumber="1087" roomClassification="" capacity="108" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
</building>
<building externalId="14Q0I41C0Z1WX1GNDC22" abbreviation="AR" locationX="40.428013" locationY="-86.916275" name="Armory">
<room externalId="14P44Y1C0WIO61GNDDFB" locationX="40.428013" locationY="-86.916275" roomNumber="101" roomClassification="classroom" capacity="48" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14P49P1C12RZ81GNDDGY" locationX="40.428013" locationY="-86.916275" roomNumber="102" roomClassification="classroom" capacity="20" instuctional="True" scheduledRoomType="teachinglab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14P4EO1C12DSF1GNDDHJ" locationX="40.428013" locationY="-86.916275" roomNumber="106" roomClassification="armory" capacity="180" instuctional="True" scheduledRoomType="specialUse">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
</building>
<building externalId="14Q0QH1C128QL1GNDC7D" abbreviation="HIKS" locationX="40.42453" locationY="-86.91265" name="John W. Hicks Undergraduate Library">
<room externalId="94185" locationX="40.42453" locationY="-86.91265" roomNumber="G959" roomClassification="" capacity="24" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
</building>
<building externalId="14Q0QW1C0XL6T1GNDC6B" abbreviation="BRNG" locationX="40.425568" locationY="-86.91625" name="Steven C. Beering Hall of Lib Arts + Ed">
<room externalId="14PIH21C10DMQ1GNDFQV" locationX="40.425568" locationY="-86.91625" roomNumber="B282" roomClassification="classLab" capacity="20" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PIHW1C102YI1GNDFQX" locationX="40.425568" locationY="-86.91625" roomNumber="B286" roomClassification="classLab" capacity="30" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PIT41C0WG5H1GNDFPF" locationX="40.425568" locationY="-86.91625" roomNumber="1242" roomClassification="classroom" capacity="30" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PITL1C12TFS1GNDFQX" locationX="40.425568" locationY="-86.91625" roomNumber="B274" roomClassification="classLab" capacity="20" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PIUF1C12ZZ81GNDFQZ" locationX="40.425568" locationY="-86.91625" roomNumber="B275" roomClassification="classLab" capacity="20" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PIWP1C12G8N1GNDFR6" locationX="40.425568" locationY="-86.91625" roomNumber="1254" roomClassification="classroom" capacity="33" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
</building>
<building externalId="14Q0V71C0WS0F1GNDC65" abbreviation="REC" locationX="40.4258" locationY="-86.9152" name="Recitation Building">
<room externalId="14PT4V1C11X0D1GNDH2N" locationX="40.4258" locationY="-86.9152" roomNumber="108" roomClassification="classroom" capacity="36" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PT5U1C103GX1GNDH5D" locationX="40.4258" locationY="-86.9152" roomNumber="315" roomClassification="classroom" capacity="30" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PTF21C0ZNTA1GNDH21" locationX="40.4258" locationY="-86.9152" roomNumber="303" roomClassification="classroom" capacity="30" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PTHO1C0ZVAH1GNDH2A" locationX="40.4258" locationY="-86.9152" roomNumber="309" roomClassification="classroom" capacity="40" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PTKG1C12MPV1GNDH5O" locationX="40.4258" locationY="-86.9152" roomNumber="225" roomClassification="classroom" capacity="28" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PTL31C12WX11GNDH5R" locationX="40.4258" locationY="-86.9152" roomNumber="226" roomClassification="classroom" capacity="30" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PTLQ1C129701GNDH5T" locationX="40.4258" locationY="-86.9152" roomNumber="227" roomClassification="classroom" capacity="28" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
</building>
<building externalId="14Q0YD1C0WWAJ1GNDC6K" abbreviation="SC" locationX="40.42656" locationY="-86.914375" name="Stanley Coulter Hall">
<room externalId="14PU4V1C0WG4N1GNDH73" locationX="40.42656" locationY="-86.914375" roomNumber="277" roomClassification="classLab" capacity="29" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PU4Y1C10YC51GNDH9Q" locationX="40.42656" locationY="-86.914375" roomNumber="102" roomClassification="classroom" capacity="35" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PU671C0WPDJ1GNDH78" locationX="40.42656" locationY="-86.914375" roomNumber="283" roomClassification="classLab" capacity="29" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
<room externalId="14PU6F1C10WUU1GNDH9W" locationX="40.42656" locationY="-86.914375" roomNumber="108" roomClassification="classroom" capacity="29" instuctional="True" scheduledRoomType="genClassroom">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
</building>
<building externalId="14Q17L1C11CKD1GNDC6I" abbreviation="WTHR" locationX="40.426373" locationY="-86.91286" name="Richard Benbridge Wetherill Lab of Chem">
<room externalId="14P0IH2VHGOQT1H7LXET" locationX="40.426373" locationY="-86.91286" roomNumber="212" roomClassification="classLab" capacity="25" instuctional="True" scheduledRoomType="computingLab">
<roomDepartments>
<assigned departmentNunber="CTRL" percent="100"/>
</roomDepartments>
</room>
</building>
</buildingsRooms>
```

# Appendix C
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE offerings PUBLIC "-//UniTime//DTD University Course Timetabling/EN" "http://www.unitime.org/interface/CourseOfferingExport.dtd">

<offerings campus="WL" year="2019" term="Fall" dateFormat="yyyy/M/d" timeFormat="HHmm" created="Sun Dec 09 17:47:35 EST 2018" includeExams="none">

<!-- same course with multiple rooms and instructors, there is one section of lab and three sections of lecture, the students must take the lab and one of the three lectures -->
  <offering id="523898" offered="true" action="insert">
       <!-- id has a 40 character limit and goes into the external id field in UniTime.  -->
	<course id="MSL10100" subject="MSL" courseNbr="10100" controlling="true" title="Foundation Officership">
  	<courseCredit creditType="collegiate" creditUnitType="semesterHours" creditFormat="fixedUnit" fixedCredit="2.0"/>
	</course>
	<config name="LecLab" limit="65">
  	<subpart type="Lab" suffix="" minPerWeek="100"/>
  	<subpart type="Lec" suffix="" minPerWeek="50"/>
  	<class id="24158" type="Lab" suffix="24158-005" limit="65" scheduleNote="MSL 101, 201, 301, 401 labs meet together" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<time days="Th" startTime="1530" endTime="1720" />
    	<room id="14P44Y1C0WIO61GNDDFB" building="AR" roomNbr="101"/>
    	<room id="14P49P1C12RZ81GNDDGY" building="AR" roomNbr="102"/>
    	<room id="14P4EO1C12DSF1GNDDHJ" building="AR" roomNbr="106"/>
    	<instructor id="12345678" fname="Frank" mname="A" lname="Sussex" share="20" lead="true" responsibility="Instructor"/>
    	<instructor id="12345679" fname="Maurice" mname="T" lname="Margo" share="20" lead="false" responsibility="Instructor"/>
    	<instructor id="12345677" fname="Abby" mname="M." lname="Gusorge" share="20" lead="false" responsibility="Instructor"/>
    	<instructor id="12345676" fname="Reggie" mname="D." lname="Thom" share="20" lead="false" responsibility="Instructor"/>
    	<instructor id="12345675" fname="Lou" mname="F." lname="Moo" share="20" lead="false" responsibility="Instructor"/>
  	</class>
  	<class id="36146" type="Lec" suffix="36146-006" limit="25" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<time days="Th" startTime="1230" endTime="1320" />
    	<room id="14P44Y1C0WIO61GNDDFB" building="AR" roomNbr="101"/>
    	<instructor id="12345677" fname="Abby" mname="M." lname="Gusorge" share="50" lead="true" responsibility="Instructor"/>
    	<instructor id="12345679" fname="Maurice" mname="T" lname="Margo" share="50" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="36147" type="Lec" suffix="36147-007" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<time days="W" startTime="1230" endTime="1320" />
    	<room id="14P49P1C12RZ81GNDDGY" building="AR" roomNbr="102"/>
    	<instructor id="12345679" fname="Maurice" mname="T" lname="Margo" share="50" lead="false" responsibility="OtherStuAccess"/>
    	<instructor id="12345677" fname="Abby" mname="M." lname="Gusorge" share="50" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="36149" type="Lec" suffix="36149-009" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<time days="T" startTime="0930" endTime="1020" />
    	<room id="14P49P1C12RZ81GNDDGY" building="AR" roomNbr="102"/>
    	<instructor id="12345679" fname="Maurice" mname="T" lname="Margo" share="50" lead="false" responsibility="OtherStuAccess"/>
    	<instructor id="12345677" fname="Abby" mname="M." lname="Gusorge" share="50" lead="true" responsibility="Instructor"/>
  	</class>
	</config>
  </offering>
<!-- This is an example of a course that has lecture, distance, and lab sections.  The sections are linked such that a specific lecture matches with a distance section which matches with a set of lab sections. -->
  <offering id="518804" offered="true" action="insert">
	<course id="EDCI27000" subject="EDCI" courseNbr="27000" controlling="true" title="Intro Ed Tech">
  	<courseCredit creditType="collegiate" creditUnitType="semesterHours" creditFormat="fixedUnit" fixedCredit="3.0"/>
	</course>
	<config name="LecLab" limit="200" instructionalMethod="B/H">
  	<subpart type="Lec" suffix="" minPerWeek="50">
    	<subpart type="Dist" suffix="" minPerWeek="50">
      	<subpart type="Lab" suffix="" minPerWeek="100"/>
    	</subpart>
  	</subpart>
  	<class id="18345" type="Lec" suffix="18345-001" limit="100" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="56791" type="Dist" suffix="56791-006" limit="100" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<class id="56796" type="Lab" suffix="56796-005" limit="25" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
        	<time days="W" startTime="1530" endTime="1720" />
        	<room id="14PU671C0WPDJ1GNDH78" building="SC" roomNbr="283"/>
        	<instructor id="87654321" fname="Meg" lname="Miamia" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<class id="18351" type="Lab" suffix="18351-002" limit="25" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
        	<time days="W" startTime="0930" endTime="1120" />
        	<room id="14PU671C0WPDJ1GNDH78" building="SC" roomNbr="283"/>
        	<instructor id="87654322" fname="Sue" mname="Prince" lname="Farmer" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<class id="18353" type="Lab" suffix="18353-003" limit="25" scheduleNote="Elementary Education, Special Education, and Early Childhood Education Learning Community students only" studentScheduling="false" displayInScheduleBook="false" cancelled="false">
        	<time days="W" startTime="1130" endTime="1320" />
        	<room id="14PU671C0WPDJ1GNDH78" building="SC" roomNbr="283"/>
        	<instructor id="87654323" fname="Jack" mname="J." lname="Sparks" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<class id="18357" type="Lab" suffix="18357-004" limit="25" scheduleNote="Secondary Education Learning Community Students only" studentScheduling="false" displayInScheduleBook="false" cancelled="false">
        	<time days="W" startTime="1330" endTime="1520" />
        	<room id="14PU671C0WPDJ1GNDH78" building="SC" roomNbr="283"/>
        	<instructor id="87654324" fname="Emmie" mname="S" lname="Marsh" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<location name="OFFCMP"/>
      	<instructor id="87654325" fname="Billy" mname="J" lname="Fish" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="M" startTime="1230" endTime="1320" />
    	<room building="WALC" roomNbr="1087"/>
    	<instructor id="87654325" fname="Billy" mname="J" lname="Fish" share="100" lead="true" responsibility="Instructor"/>
    	<instructor id="87654326" fname="Anita" lname="Cane" share="0" lead="true" responsibility="OtherStuAccess"/>
  	</class>
  	<class id="56790" type="Lec" suffix="56790-010" limit="100" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="56792" type="Dist" suffix="56792-015" limit="100" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<class id="18355" type="Lab" suffix="18355-012" limit="25" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
        	<time days="W" startTime="1130" endTime="1320" />
        	<room id="14PU4V1C0WG4N1GNDH73" building="SC" roomNbr="277"/>
        	<instructor id="87654324" fname="Emmie" mname="S" lname="Marsh" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<class id="56794" type="Lab" suffix="56794-013" limit="25" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
        	<time days="W" startTime="1330" endTime="1520" />
        	<room id="14PU4V1C0WG4N1GNDH73" building="SC" roomNbr="277"/>
        	<instructor id="87654327" fname="Hannah" lname="Smith" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<class id="56795" type="Lab" suffix="56795-014" limit="25" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
        	<time days="W" startTime="1530" endTime="1720" />
        	<room id="14PU4V1C0WG4N1GNDH73" building="SC" roomNbr="277"/>
        	<instructor id="87654328" fname="Jane" lname="Pettit" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<class id="11195" type="Lab" suffix="11195-011" limit="25" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
        	<time days="W" startTime="0930" endTime="1120" />
        	<room id="14PU4V1C0WG4N1GNDH73" building="SC" roomNbr="277"/>
        	<instructor id="87654323" fname="Jack" mname="J." lname="Sparks" share="100" lead="true" responsibility="Instructor"/>
      	</class>
      	<location name="OFFCMP"/>
      	<instructor id="87654325" fname="Billy" mname="J" lname="Fish" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="M" startTime="1130" endTime="1220" />
    	<room building="WALC" roomNbr="1087"/>
    	<instructor id="87654326" fname="Anita" lname="Cane" share="0" lead="true" responsibility="Instructor"/>
    	<instructor id="87654325" fname="Billy" mname="J" lname="Fish" share="100" lead="true" responsibility="Instructor"/>
  	</class>
	</config>
  </offering>
<!-- This is a sample of how to define sections if they are packaged in Banner. Note that the class ids of all sections list the same crn and they all are mapped to the same instructional type.  You may want to create a configuration per packaged section if the minutes per week are not consistent for the pieces of the section.  -->
  <offering id="519636" offered="true" action="insert">
	<course id="ENGL10800" subject="ENGL" courseNbr="10800" controlling="true" title="Accel First-Yr Compos" scheduleBookNote="Engaging in Public Discourse - An accelerated composition course that substitutes for English 10600 in which students will engage in public writing. ">
  	<courseCredit creditType="collegiate" creditUnitType="semesterHours" creditFormat="fixedUnit" fixedCredit="3.0"/>
	</course>
	<config name="MWF" limit="140">
  	<subpart type="Lec" suffix="" minPerWeek="100">
    	<subpart type="Lec" suffix="a" minPerWeek="50"/>
  	</subpart>
  	<class id="21384" type="Lec" suffix="21384-048" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21384" type="Lec" suffix="21384-048" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="F" startTime="0930" endTime="1020" />
      	<room id="14PITL1C12TFS1GNDFQX" building="BRNG" roomNbr="B274"/>
      	<instructor id="56789123" fname="Ed" mname="E" lname="Snerk" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="MW" startTime="0930" endTime="1020" />
    	<room id="14PT4V1C11X0D1GNDH2N" building="REC" roomNbr="108"/>
    	<instructor id="56789123" fname="Ed" mname="E" lname="Snerk" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="21385" type="Lec" suffix="21385-049" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21385" type="Lec" suffix="21385-049" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="W" startTime="1430" endTime="1520" />
      	<room id="14PITL1C12TFS1GNDFQX" building="BRNG" roomNbr="B274"/>
      	<instructor id="56789124" fname="Gus" lname="Hans" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="MF" startTime="1430" endTime="1520" />
    	<room id="14PT4V1C11X0D1GNDH2N" building="REC" roomNbr="108"/>
    	<instructor id="56789124" fname="Gus" lname="Hans" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="21386" type="Lec" suffix="21386-050" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21386" type="Lec" suffix="21386-050" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="M" startTime="1130" endTime="1220" />
      	<room id="14PITL1C12TFS1GNDFQX" building="BRNG" roomNbr="B274"/>
      	<instructor id="56789125" fname="Tavia" mname="James" lname="Richards" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="WF" startTime="1130" endTime="1220" />
    	<room id="14PTKG1C12MPV1GNDH5O" building="REC" roomNbr="225"/>
    	<instructor id="56789125" fname="Tavia" mname="James" lname="Richards" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="21387" type="Lec" suffix="21387-051" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21387" type="Lec" suffix="21387-051" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="M" startTime="1530" endTime="1620" />
      	<room id="14PIH21C10DMQ1GNDFQV" building="BRNG" roomNbr="B282"/>
      	<instructor id="56789126" fname="Kim" mname="W." lname="Cook" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="WF" startTime="1530" endTime="1620" />
    	<room id="14PT4V1C11X0D1GNDH2N" building="REC" roomNbr="108"/>
    	<instructor id="56789126" fname="Kim" mname="W." lname="Cook" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="21388" type="Lec" suffix="21388-052" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21388" type="Lec" suffix="21388-052" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="F" startTime="1230" endTime="1320" />
      	<room id="14PIH21C10DMQ1GNDFQV" building="BRNG" roomNbr="B282"/>
      	<instructor id="56789127" fname="Janice" mname="Anne" lname="Orville" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="MW" startTime="1230" endTime="1320" />
    	<room id="14PTKG1C12MPV1GNDH5O" building="REC" roomNbr="225"/>
    	<instructor id="56789127" fname="Janice" mname="Anne" lname="Orville" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="21389" type="Lec" suffix="21389-053" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21389" type="Lec" suffix="21389-053" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="M" startTime="1430" endTime="1520" />
      	<room id="14PIH21C10DMQ1GNDFQV" building="BRNG" roomNbr="B282"/>
      	<instructor id="56789128" fname="Betty" mname="Annabelle" lname="Powers" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="WF" startTime="1430" endTime="1520" />
    	<room id="14PTL31C12WX11GNDH5R" building="REC" roomNbr="226"/>
    	<instructor id="56789128" fname="Betty" mname="Annabelle" lname="Powers" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="21395" type="Lec" suffix="21395-054" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21395" type="Lec" suffix="21395-054" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="W" startTime="0830" endTime="0920" />
      	<room id="14PIUF1C12ZZ81GNDFQZ" building="BRNG" roomNbr="B275"/>
      	<instructor id="56789129" fname="Harry" mname="M" lname="Tale" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="MF" startTime="0830" endTime="0920" />
    	<room id="14PT4V1C11X0D1GNDH2N" building="REC" roomNbr="108"/>
    	<instructor id="56789129" fname="Harry" mname="M" lname="Tale" share="100" lead="true" responsibility="Instructor"/>
  	</class>
	</config>
	<config name="TTH" limit="140">
  	<subpart type="Lec" suffix="" minPerWeek="75">
    	<subpart type="Lec" suffix="a" minPerWeek="75"/>
  	</subpart>
  	<class id="15677" type="Lec" suffix="15677-038" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="15677" type="Lec" suffix="15677-038" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="T" startTime="1500" endTime="1615" />
      	<room id="14PITL1C12TFS1GNDFQX" building="BRNG" roomNbr="B274"/>
      	<instructor id="67891234" fname="Sarah" mname="M" lname="Ludwig" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="Th" startTime="1500" endTime="1615" />
    	<room id="14PTF21C0ZNTA1GNDH21" building="REC" roomNbr="303"/>
    	<instructor id="67891234" fname="Sarah" mname="M" lname="Ludwig" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="15678" type="Lec" suffix="15678-039" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="15678" type="Lec" suffix="15678-039" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="Th" startTime="1030" endTime="1145" />
      	<room id="14PIH21C10DMQ1GNDFQV" building="BRNG" roomNbr="B282"/>
      	<instructor id="67891235" fname="Fred" mname="T" lname="Ham" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="T" startTime="1030" endTime="1145" />
    	<room id="14PTLQ1C129701GNDH5T" building="REC" roomNbr="227"/>
    	<instructor id="67891235" fname="Fred" mname="T" lname="Ham" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="21415" type="Lec" suffix="21415-055" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="21415" type="Lec" suffix="21415-055" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="Th" startTime="1200" endTime="1315" />
      	<room id="14PITL1C12TFS1GNDFQX" building="BRNG" roomNbr="B274"/>
      	<instructor id="67891234" fname="Sarah" mname="M" lname="Ludwig" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="T" startTime="1200" endTime="1315" />
    	<room id="14PT5U1C103GX1GNDH5D" building="REC" roomNbr="315"/>
    	<instructor id="67891234" fname="Sarah" mname="M" lname="Ludwig" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="23078" type="Lec" suffix="23078-056" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="23078" type="Lec" suffix="23078-056" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="Th" startTime="1500" endTime="1615" />
      	<room id="14P0IH2VHGOQT1H7LXET" building="WTHR" roomNbr="212"/>
      	<instructor id="67891236" fname="Alice" mname="J" lname="Trail" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="T" startTime="1500" endTime="1615" />
    	<room id="14P0IH2VHGOQT1H7LXET" building="WTHR" roomNbr="212"/>
    	<instructor id="67891236" fname="Alice" mname="J" lname="Trail" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="23380" type="Lec" suffix="23380-059" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="23380" type="Lec" suffix="23380-059" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="Th" startTime="1200" endTime="1315" />
      	<room id="14PIHW1C102YI1GNDFQX" building="BRNG" roomNbr="B286"/>
      	<instructor id="67891237" fname="Gina" lname="Brant" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="T" startTime="1200" endTime="1315" />
    	<room id="14PTHO1C0ZVAH1GNDH2A" building="REC" roomNbr="309"/>
    	<instructor id="67891237" fname="Gina" lname="Brant" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="23381" type="Lec" suffix="23381-060" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="23381" type="Lec" suffix="23381-060" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="Th" startTime="1500" endTime="1615" />
      	<room id="14PIWP1C12G8N1GNDFR6" building="BRNG" roomNbr="1254"/>
      	<instructor id="67891237" fname="Gina" lname="Brant" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="T" startTime="1500" endTime="1615" />
    	<room building="HIKS" roomNbr="G959"/>
    	<instructor id="67891237" fname="Gina" lname="Brant" share="100" lead="true" responsibility="Instructor"/>
  	</class>
  	<class id="23378" type="Lec" suffix="23378-058" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
    	<class id="23378" type="Lec" suffix="23378-058" limit="20" studentScheduling="true" displayInScheduleBook="true" cancelled="false">
      	<time days="Th" startTime="1630" endTime="1745" />
      	<room id="14PIT41C0WG5H1GNDFPF" building="BRNG" roomNbr="1242"/>
      	<instructor id="67891237" fname="Gina" lname="Brant" share="100" lead="true" responsibility="Instructor"/>
    	</class>
    	<time days="T" startTime="1630" endTime="1745" />
    	<room building="HIKS" roomNbr="G959"/>
    	<instructor id="67891237" fname="Gina" lname="Brant" share="100" lead="true" responsibility="Instructor"/>
  	</class>
	</config>
  </offering>
</offerings>
```

# Appendix D

```
<request campus="WL" year="2019" term="Fall">
  <student key="78912345">
	<updateDemographics>
  	<name first="Abby" middle="S" last="Miller"/>
  	<acadArea abbv="PI" classification="01">
    	<major code="ALMO"/>
  	</acadArea>
  	<groupAffiliation code="STAR"/>
  	<groupAffiliation code="STAR-06/21"/>
	</updateDemographics>
	<updateCourseRequests commit="true">
  	<courseOffering subjectArea="SCLA" courseNumber="10100">
    	<alternative subjectArea="ENGL" courseNumber="10600">
      	<alternative subjectArea="ENGL" courseNumber="10800"/>
    	</alternative>
  	</courseOffering>
  	<courseOffering subjectArea="AT" courseNumber="10000"/>
  	<courseOffering subjectArea="MA" courseNumber="16010"/>
  	<courseOffering subjectArea="TECH" courseNumber="12000R"/>
  	<courseOffering subjectArea="PSY" courseNumber="12000">
    	<alternative subjectArea="SOC" courseNumber="10000"/>
  	</courseOffering>
  	<courseOffering subjectArea="SCLA" courseNumber="10200" alternative="true"/>
	</updateCourseRequests>
  </student>
  <student key="78912344">
	<updateDemographics>
  	<name first="Allen" middle="L" last="Potter"/>
  	<acadArea abbv="PI" classification="01">
    	<major code="ANIM"/>
  	</acadArea>
  	<groupAffiliation code="STAR"/>
  	<groupAffiliation code="STAR-07/10"/>
	</updateDemographics>
	<updateCourseRequests commit="true">
  	<courseOffering subjectArea="CGT" courseNumber="10101"/>
  	<courseOffering subjectArea="CGT" courseNumber="11800"/>
  	<courseOffering subjectArea="TECH" courseNumber="12000H">
    	<alternative subjectArea="PSY" courseNumber="12000">
      	<alternative subjectArea="AAS" courseNumber="27100"/>
    	</alternative>
  	</courseOffering>
  	<courseOffering subjectArea="SCLA" courseNumber="10100"/>
  	<courseOffering subjectArea="HONR" courseNumber="19901">
    	<preferences>
      	<class externalId="11580" type="Lec" suffix="11580-024"/>
    	</preferences>
  	</courseOffering>
  	<courseOffering subjectArea="MA" courseNumber="15800"/>
	</updateCourseRequests>
  </student>
</request>
```