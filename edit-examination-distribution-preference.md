---
layout: default
title: Edit Examination Distribution Preference
---


## Screen Description

The Edit Examination Distribution Preference screen provides user interface for editing an existing distribution preference between midterm or final examinations.

![Edit Examination Distribution Preference](images/edit-examination-distribution-preference-1.png){:class='screenshot'}

## Details

### Edit Examination Distribution Preference

* **Distribution Type**
    * Type of distribution preference
    * When a type is selected, its description is displayed right below the drop-down list
    * Possible types
        * **Precedence**
            * Exams are to be placed in the given order.
            * When prohibited or (strongly) discouraged: exams are to be placed in the order reverse to the given one.
        * **Same Period**
            * Exams are to be placed in the same period.
            * When prohibited or (strongly) discouraged: exams are to be placed at different periods.
        * **Same Room**
            * Exams are to be placed in the same room(s).
            * When prohibited or (strongly) discouraged, exams are to be placed in different rooms.
        * **Share Room**
            * Given examinations can share a room (use the same room during the same period) if the room is big enough.
            * If examinations of different seating types are sharing a room, the more restrictive seating type is used to check the room size.
        * **Same Day** (optional)
            * Exams are to be placed on the same day.
            * When prohibited or (strongly) discouraged: exams are to be placed on different days.
            * Not available by default, needs to be registered with the [Examination Same Day Constraint.xml](https://github.com/UniTime/unitime/commits/master/Documentation/Scripts/Examination%20Same%20Day%20Constraint.xml) script. To register, download the XML file and import it on the [Data Exchange](data-exchange) page, then run the Distribution Types: Same Day (Examination) script on the [Scripts](scripts) page.
* **Preference**
    * Preference level - a scale ranging from prohibited to required

### Midterm/Final Examinations in Distribution

* Operation: **Add Examination**
	* Add another line with drop down lists in which you can select another examination

* The three drop down lists on each line are for
	1. Subject area
	2. Course number
	3. Examination name

* The up ![Up](images/icon-up.png) and down ![Down](images/icon-down.png) arrows can be used to change the order of classes if order is important (for example, when the Distribution Type "Precedence" is used)
* You can delete any of the lines with classes by clicking on the ![Delete](images/icon-delete.png) icon at the end of the line

## Operations

* **Update** (ALT+U)
	* Save changes and go back to the previous screen

* **Delete** (ALT+D)
	* Delete the distribution preference and go back to the previous screen

* **Back** (ALT+B)
	* Go back to the previous screen without saving any changes

