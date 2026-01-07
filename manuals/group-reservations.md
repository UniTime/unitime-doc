---
layout: manual
title: Managing Student Group Reservations
updated: Janury 2026
---

### Table of Contents
{:.no_toc}
* table
{:toc}

Student group reservations are used to ensure a specific set of students are scheduled in a specific course section.  This document describes the process of creating student group reservations.

# Student Group Types

Student group types can be created to organize student groups and assign additional meaning to a student group.  To create a student group type go to the **Administration > Other > [Student Group Types](../student-group-types)** page.

![Managing Student Group Reservations](images/group-reservations-1.png){:class='screenshot'}

Press the **Add** button to go to the Add Student Group Types page.

![Managing Student Group Reservations](images/group-reservations-2.png){:class='screenshot'}


The following fields may be populated for a student group:

* **Code:**  A short name for the student group type
* **Name:**  A long name for the student group type
* **Keep Students Together:**  This should be checked if it is desired that the student sectioning solver try to put students of this type of group into the same sections when they request the same courses.
* **Disabled Sections:** This determines how to handle the students in groups of this type in relation to sections that are *Disabled for Student Scheduling*.  This is the equivalent of “No Print” in Banner.  For the student scheduling solver to place a student into one of these sections special handling is required.
	* **Not Allowed:** Students in student groups of this type are not allowed to be placed in a section that is *Disabled for Student Scheduling*.
	* **Allowed with Group Reservation:**  Students in student groups of this type are allowed to be placed in a section that is *Disabled for Student Scheduling* if there is a corresponding student group reservation.
	* **Always Allowed:**  Students in student groups of this type are allowed to be placed in a section that is *Disabled for Student Scheduling*.
* **Advisors Can Set:** This should be checked if advisors are assigned to students within the system and advisors should have the ability to assign students to the student groups of this type using the Online Student Scheduling Dashboard.

![Managing Student Group Reservations](images/group-reservations-3.png){:class='screenshot'}

Once the data for the student group type is entered, press the **Save** button to save the group and return to the [Student Group Types](../student-group-types) page.

![Managing Student Group Reservations](images/group-reservations-4.png){:class='screenshot'}

The student group type is visible on the [Student Group Types](../student-group-types) page and available to be used for student group reservations.  Clicking on the student group will take you to the [Edit Student Group Types](../edit-student-group-types) page.

![Managing Student Group Reservations](images/group-reservations-5.png){:class='screenshot'}

This [Edit Student Group Types](../edit-student-group-types) page can be used to edit the data associated with the group type.

# Student Groups

Student groups are used to represent a set of students who for any number of reasons need to be grouped together.

To create a student group go to the *Administration > Academic Sessions > [Student Groups](../student-groups)* page.

![Managing Student Group Reservations](images/group-reservations-6.png){:class='screenshot'}

Press the **Add** button to go to the [Add Student Group](../add-student-group) page.

![Managing Student Group Reservations](images/group-reservations-7.png){:class='screenshot'}

The following fields may be populated for a student group:
* **Code:** A short code to identify the group.
* **Name:** A longer name to identify the group
* **Type:** If student groups types have been defined, a type can be selected.
* **Expected Size:** If the expected size of the group is known, it may be entered here.  This is useful when the full list of students associated with the group is not known yet.
* **Students:** The list ids of the students who are part of the group.  Enter one id per line. This can be left blank during creation of the group and populated later.

![Managing Student Group Reservations](images/group-reservations-8.png){:class='screenshot'}

*Note:* It is possible to paste a long list of students into the Students text box rather than typing them individually.

The **Lookup** button at the lower right hand side of the Students text box can be used to search for students to add to the group.

![Managing Student Group Reservations](images/group-reservations-9.png){:class='screenshot'}

Typing in the name field at the top of the dialog search the students table for matches.  When a student name is double clicked, the student id is added to the student list on the [Add Student Group](../add-student-group) page.

![Managing Student Group Reservations](images/group-reservations-10.png){:class='screenshot'}

Once the data for the student group is entered, press the **Save** button to save the group and return to the [Student Groups](../student-groups) page.

![Managing Student Group Reservations](images/group-reservations-11.png){:class='screenshot'}

The student group is visible on the Student Groups page and available to be used for student group reservations.  Clicking on the student group will take you to the [Edit Student Group](../edit-student-group) page.

![Managing Student Group Reservations](images/group-reservations-12.png){:class='screenshot'}

This [Edit Student Group](../edit-student-group) page can be used to edit the list of students associated with the group.

# Student Group Reservations

[Student Group Reservations](../reservations) are used to reserve space for students belong to a [Student Group](../student-groups) to a particular course.  The reservations can be set at the course level, the configuration level, or the individual class level.

To create a student group reservation go to the **Courses > Input Data > [Instructional Offerings](../instructional-offerings)** page.

![Managing Student Group Reservations](images/group-reservations-13.png){:class='screenshot'}

Select the Subject Area and enter the Course Number for the course to which to add the reservation and press the **Search** button.  This will take you to the [Instructional Offering Detail](../instructional-offering-detail) page for that course.

![Managing Student Group Reservations](images/group-reservations-14.png){:class='screenshot'}

Press the **Add Reservation** button to go to the [Add Reservation](../add-reservation) page.

![Managing Student Group Reservations](images/group-reservations-15.png){:class='screenshot'}

The following fields may be populated for a student group:
* **Instructional Offering:** The course associated with the reservation.
* **Type:** The type of reservation to apply.  Select *Student Group Reservation* to add a student group reservation.  This will at the *Student Group* field as an option.
* **Reserved Space:** The number of seats to be reserved for this reservation.  If this is left blank, all seats in the classes associated with the reservation will be held for students belonging to the selected student group.
* **Expiration Date:** The date the reservation expires and other students are allowed to be scheduled into seats held by this reservation.  If left blank, the reservation never expires.
* **Restrictions:**  If the reservation does not apply to the entire course, the configuration(s) and/or classes(s) it applies to can be selected here.  Pressing the ![+](../images/icon-filter-open.gif) or ![-](../images/icon-filter-close.gif) icon next to each configuration hides or shows the sections associated with the configurations.  Selecting a checkbox next to a configuration or class designates it as the configuration or class used by the students associated with the reservation.  Multiple selections can be made.
* **Student Group:**  The student group associated with the reservation.

![Managing Student Group Reservations](images/group-reservations-16.png){:class='screenshot'}

Once the reservation is configured press the **Save** button to save it and return to the [Instructional Offering Detail](../instructional-offering-detail) page.

The student group reservation is visible on the [Instructional Offering Detail](../instructional-offering-detail) page and will be used by the student sectioning solver in determining where to place the students associated with the student group.

![Managing Student Group Reservations](images/group-reservations-17.png){:class='screenshot'}

Clicking on the student group reservation will take you to the [Edit Reservation](../edit-reservation) page.

![Managing Student Group Reservations](images/group-reservations-18.png){:class='screenshot'}

This [Edit Reservation](../edit-reservation) page can be used to edit the details of the reservation.


