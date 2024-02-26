---
layout: manual
title: UniTime Exports
version: 4.4.91
updated: April, 2019
---

### Table of Contents
{:.no_toc}
* table
{:toc}

# Authentication

Export calls can use HTTP-simple authentication with a user created using the UniTime’s [Users](../users-database-authentication) page, or if enabled (by setting the application property unitime.api.canUseToken to true) it can authenticated via an API token. The API token can be passed as an additional attribute (named ***token***) on any export call. The user must have a default role with the appropriate export permission (in general, the user must have the same permissions as to be able to do the export in UniTime). The API token is available on the Users page (when enabled), it is computed using the username and hashed password (changing password will also change the API token for a user).

All export are using the export servlet (e.g., `GET UniTime/export?output=<format>`), with the mandatory **output** parameter specifies the type and format of the export. Additional parameters based on the export may be provided. Most exports require to specify the academic session at the very least (**sid** parameter containing unique id of the academic session or term parameter containing `<term><year><initiative>`, e.g., Fal2010woebegon; the initiative can be omitted if there is only one initiative for the given term and year, e.g., Fal2010).

# CSV Format

When a CSV is being exported csvDelimiter and csvQuotation parameters can be used to define delimiter and quotations in the resultant file.

# 1 Events

The UniTime events can be exported in iCalendar, CSV, or PDF format. The following outputs are allowed:

* events.ics (iCalendar format)
* events.csv (CSV format from the List of Events)
* events.pdf (PDF format from the List of Events)
* meetings.csv (CSV format from the List of Meetings)
* meetings.pdf (PDF format from the List of Meetings)

The URL has to have a **type** parameter specified, which could be:

* room (for room timetable)
* subject (for subject timetable)
* curriculum (for curriculum timetable)
* department (for department timetable)
* person (for personal schedule)
* course (for course schedule)
* group (for student group schedule)

If type is not room, the resource has to be specified either using its UniTime unique id (**id** parameter), by its external id (**ext** parameter for room and person), or by its reference (**name** parameter for all types but room and person).

Event unavailabilities can be included by adding setting the **ua** parameter to 1.

CSV and PDF exports can define which columns are to be included (**flags** parameter, set to -1 for all columns) and how the table is to be sorted (**sort** parameter, containing index of the column starting with 1, negative index for descending order). The flags parameter is a sum of the following bits:

* 1 … SHOW_PUBLISHED_TIME
* 2 … SHOW_ALLOCATED_TIME
* 4 … SHOW_SETUP_TIME
* 8 … SHOW_TEARDOWN_TIME
* 16 … SHOW_CAPACITY
* 32 … SHOW_LIMIT
* 64 … SHOW_ENROLLMENT
* 128 … SHOW_MAIN_CONTACT
* 256 … SHOW_SPONSOR
* 512 … SHOW_SECTION
* 1024 … SHOW_TITLE
* 2048 … SHOW_APPROVAL
* 4096 … SHOW_NOTE
* 8192 … SHOW_LAST_CHANGE
* 16384 … SHOW_MEETING_CONTACTS

The exported events / meetings can be filtered down by any mean that could be used in the [Event Filter](../events-event-filter) and [Room Filter](../events-room-filter) components. In general, all chips of the event filter are prefixed with e: (e:text is the remaining text, if present) and all chips of the room filter are prefixed with r: (r:text is the remaining text, if present). Here are a few examples:

* e:type=Final+Exam   (final examination event type)
* e:flag=All+Sessions  (span the search across all sessions of the matching campus)
* e:from=1/31/2017   (only meetings from January 31, 2017)
* r:type=Classrooms   (only meetings in classroom -- that is rooms of type Classrooms)
* r:feature=Piano   (only rooms with Piano feature)
* r:text=EDUC+101   (only in EDUC 101 room)

**Tip:** use locale=en_UK for having the times in 24h format and dates in the (day.month.year format).


Example iCalendar schedule for a student with external id 1001

[https://demo.unitime.org/UniTime/export?output=events.ics&type=PERSON&ext=1001&term=Fal2010&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh](https://demo.unitime.org/UniTime/export?output=events.ics&type=PERSON&ext=1001&term=Fal2010&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh)


All events in EDUC 101 of the current academic session in CSV format:

[https://demo.unitime.org/UniTime/export?output=events.csv&type=room&r:text=EDUC+101&flags=-1](https://demo.unitime.org/UniTime/export?output=events.csv&type=room&r:text=EDUC+101&flags=-1)
 
All examination meetings in EDUC 101 of the given academic session in PDF format:

[https://demo.unitime.org/UniTime/export?output=meetings.pdf&type=room&e:type=Midterm+Exam&e:type=Final+Exam&r:text=EDUC+101&term=Fal2010woebegon](https://demo.unitime.org/UniTime/export?output=meetings.pdf&type=room&e:type=Midterm+Exam&e:type=Final+Exam&r:text=EDUC+101&term=Fal2010woebegon)

Class schedule of the first year of A/M1 curriculum

[https://demo.unitime.org/UniTime/export?output=events.pdf&type=curriculum&name=A/M1+01&term=Fal2010&e:type=Class](https://demo.unitime.org/UniTime/export?output=events.pdf&type=curriculum&name=A/M1+01&term=Fal2010&e:type=Class)

# 2 HQL Reports

The HQL reports can be exported form UniTime in CSV format using output=hql-report.csv, or JSON format using output=hql-reports.json. These are, for instance, the reports available on the Courses > Reports page. HQL appearance and admin-only permissions are checked (the user must have the appropriate permissions to be able to get the report).


The **report** parameter can contain name of the report or its unique id. Individual report parameters can be looked up, for example:

* DEPARTMENT=<deptCode>
* SUBJECT=<abbreviation>
* ROOM=<name>
* RoomType=<reference>

The following example returns results of the New Courses report for ALG and BIOL subject areas on our online demo:

[https://demo.unitime.org/UniTime/export?output=hql-report.csv&report=New+Courses&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh&term=Fal2010&SUBJECTS=ALG&SUBJECTS=BIOL](https://demo.unitime.org/UniTime/export?output=hql-report.csv&report=New+Courses&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh&term=Fal2010&SUBJECTS=ALG&SUBJECTS=BIOL)

# 3 Rooms

The rooms, room groups and room features can be exported in CSV or PDF format, based on the **output** parameter:

* rooms.pdf   (rooms in PDF format)
* rooms.csv  (rooms in CSV format)
* rooms.json   (rooms in JSON format)
* roomfeatures.csv, roomfeatures.pdf (room features in CSV or PDF format respectively)
* roomgroups.csv, roomgroups.pdf  (room groups in CSV or PDF format respectively)

Same as in the events, the room filter parameters can be included in the URL, with the r: prefix.

The departments can be exported in the following format (based on the **dm** parameter):

* 0 … use department code only
* 1 … use department abbreviation
* 2 … use department label / name
* 3 … use department abbreviation - department name
* 4 … use department code - department name

The table can be sorted by any column using **sort** parameter (contain index of the column, starting from 1, negative numbers for descendant order).

The **flags** parameter can be used to define which columns are to be included in the exported table. The **orientation** can be used to define how the room sharing is to be exported (it can contain text, vertical, or horizontal). Parameter **mode** can be used to select which of the available modes is to be used for the room sharing grid (e.g., Workdays × Daytime). Parameter **department** can be used to select department (contains department code).

The **flags** parameter can contain a combination of the following columns:

* 1 … NAME
* 2 … EXTERNAL_ID
* 4 … TYPE
* 8 … CAPACITY
* 16 … EXAM_CAPACITY
* 32 … AREA
* 64 … COORDINATES
* 128 … DISTANCE_CHECK
* 256 … ROOM_CHECK
* 512 … MAP
* 1024 … PICTURES (+1 for each attachment type)
* 2048 … Other Attachments
* 4096 … Pictures
* 8192 … PREFERENCE
* 16384 … AVAILABILITY
* 32768 … DEPARTMENTS
* 65536 … CONTROL_DEPT
* 131072 … EXAM_TYPES
* 262144 … PERIOD_PREF
* 524288 … EVENT_DEPARTMENT
* 1048576 … EVENT_STATUS
* 2097152 … EVENT_AVAILABILITY
* 4194304 … EVENT_MESSAGE
* 8388608 … BREAK_TIME
* 16777216 … GROUPS
* 33554432 … FEATURES (+1 for each room feature type)

Examples:

[http://demo.unitime.org/UniTime/export?output=roomfeatures.csv&r:type=Classrooms&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh](http://demo.unitime.org/UniTime/export?output=roomfeatures.csv&r:type=Classrooms&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh)

[http://demo.unitime.org/UniTime/export?output=rooms.pdf&r:feature=Comp&r:building=EDUC&dm=4&orientation=horizontal&flags=52084765&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh](http://demo.unitime.org/UniTime/export?output=rooms.pdf&r:feature=Comp&r:building=EDUC&dm=4&orientation=horizontal&flags=52084765&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh)

# 4 Student Scheduling Solver Reports

The student scheduling reports can be exported from the Online Student Scheduling Reports page (when output=sct-report.csv&online=true), from the Student Sectioning Solver Reports (when `output=sct-report.csv&online=false` for the solver of the user running the export, or the from the published solver when online parameter is not used).

Example:

[https://demo.unitime.org/UniTime/export?output=sct-report.csv&name=TABLEAU_REPORT&term=Fal2010&online=true&pritify=false&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh](https://demo.unitime.org/UniTime/export?output=sct-report.csv&name=TABLEAU_REPORT&term=Fal2010&online=true&pritify=false&token=1xhp5vo3zfxrpbzjzhtanmcipolx03fv42ohz4xa507x5acydh)


```
curl -u admin:admin "https://demo.unitime.org/UniTime/export?output=sct-report.csv&name=TABLEAU_REPORT&term=Fal2010&online=true&pritify=false"
```

Parameter `pritify=false` will tell UniTime to avoid putting blank spaces on repeating cells.

Available reports are listed in the [SectioningReportTypesBackend.ReportType](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/server/sectioning/SectioningReportTypesBackend.java#L59) enum.
