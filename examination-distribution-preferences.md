---
layout: default
title: Examination Distribution Preferences
---


## Screen Description

The Examination Distribution Preferences screen provides a list of distribution preferences related to either midterm or final examinations.

![Examination Distribution Preferences](images/examination-distribution-preferences-1.png){:class='screenshot'}

## Details

The following criteria can be used to specify what distribution preferences should be listed.


* **Type**
    * Type of the examination (e.g., midterm or final)

* **Subject**
    * Subject area

* **Course Number**
    * Course number or a "wild card" (such as "2*" for all courses starting with 2)

Distribution preferences can be also filtered by preference or distribution type. To do so, open the **Filter** by clicking the ![Open Filter](images/icon-filter-open.gif) icon.

Click the **Search** button to apply any changes to the search criteria.

The list of distribution preferences has the following columns.

* **Type**
    * Type of distribution preference
    * Possible types
        * **Precedence**
            * Exams are to be placed in the given order.
            * When prohibited or (strongly) discouraged: exams are to be placed in the order reverse to the given one.
        * **Same Period**
            * Exams are to be placed in the same period.
            * When prohibited or (strongly) discouraged: exams are to be placed at different periods.
        * **Same Room**
            * Exams are to be placed in the same room(s).
            * When prohibited or (strongly) discouraged: exams are to be placed at different rooms.
        * **Share Room**
            * Given examinations can share a room (use the same room during the same period) if the room is big enough.
            * If examinations of different seating types are sharing a room, the more restrictive seating type is used to check the room size.
        * **Same Day** (optional)
            * Exams are to be placed on the same day.
            * When prohibited or (strongly) discouraged: exams are to be placed on different days.
            * Not available by default, needs to be registered with the [Examination Same Day Constraint.xml](https://github.com/UniTime/unitime/blob/master/Documentation/Scripts/Examination%20Same%20Day%20Constraint.xml) script. To register, download the XML file and import it on the [Data Exchange](data-exchange) page, then run the Distribution Types: Same Day (Examination) script on the [Scripts](scripts) page.

* **Examination**
    * The name of the examination (it is automatically generated from the classes/courses names unless overridden by the user in the [Edit Examination](edit-examination) screen)

* **Classes / Courses**
    * Instructional components (offerings, courses, configurations, classes) associated with the examination

Click on any distribution preference to get to the [Edit Examination Distribution Preference](edit-examination-distribution-preference) screen.

## Operations

* **Export**
    * Export the list of distribution preferences into a file (PDF, XLS, or CSV)

* **Add Distribution Preference** (ALT+A)
    * Go to the [Add Examination Distribution Preference](add-examination-distribution-preference) screen to add a new distribution preference

