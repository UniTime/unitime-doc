---
layout: default
title: Instructors
---


## Screen Description

The Instructors screen displays a list of instructors that can be used throughout the application, for example, to assign instructors to classes or examinations. Clicking on any instructor will take you to their [Instructor Detail](instructor-detail) screen.

![Instructors](images/instructors-1.png){:class='screenshot'}

## Top Line with Search

* **Department**
    * The department for which you want to view a list of instructors. If you are responsible for more than one department, you will need to select a department in the drop-down list and click on **Search** (Alt+S)
    * If you are responsible for only one department, this field will be pre-populated for you

* **Filter**
    * **Position** It is possible to filter the list of instructors by the instructor position or positions. 

* **Export CSV** (Alt+C), **Export XLS** (Alt+X), **Export PDF** (Alt+P)
    * You can export your list of instructors into a CSV/XLS/PDF document

* **Survey XLS** (Alt+X)
    * Export filled-in instructor surveys in an XLS format

* **Manage Instructor List** (Alt+M)
    * Go to the [Manage Instructor List](manage-instructor-list) screen, which allows you to import staff members or remove instructors from your list

* **Add New Instructor** (Alt+A)
    * Go to the [Add Instructor](add-instructor) screen to add a new instructor

## Details

For each instructor, you can see

* **External Id**
    * Instructor's Id as used in other systems; used to identify instructors throughout UniTime
    * If the instructor does not have an External Id assigned, or you have not yet matched the instructor to their Id, you will see a warning ![Warning](images/icon-error.png) icon in this column
    * To find instructor's External Id, go to the [Edit Instructor](edit-instructor) screen and click on the Lookup button

* **Name**
    * Name of the instructor
    * To change the format in which names are displayed, click on "Settings" under "Preferences" in the main menu; this takes you to the [Manager Settings](manager-settings) screen.

* **Position**
    * Position classification of this instructor
    * Note: This field is user-maintained and is not required elsewhere in UniTime. It may be useful, however, for grouping instructors or in exports for departmental reports.

* **Note**
    * Note on the instructor
    * For your use only (you can enter anything you want here, and this note will not be used elsewhere)
    * To change the note, go to the [Edit Instructor](edit-instructor) screen

* **Preferences**
    * **Time**, **Room**, **Distribution**, and **Course** preferences of the instructor
    * Instructor preferences are optional; they may be set up using the [Instructor Preferences](instructor-preferences) screen (accessible from the [Instructor Detail](instructor-detail) screen)
    * The preferences will be considered only for those classes on which the "conflict checking" is turned on for the instructor (this can be changed, e.g., in the [Edit Class](edit-class) screen)
    * Course preferences are only used in the [Instructor Scheduling](instructor-scheduling.md)

* **Teaching Preference**
    * Teaching preferences are used in the [Instructor Scheduling](instructor-scheduling.md) and edited on the [Instructor Assignment Preferences](instructor-assignment-preferences) page
    * This column is only displayed when there is at least one instructor in the department with a teaching preference set

* **Unavailable Dates**
    * List of dates during which the instructor is not available (cannot teach)

* **Maximal Load**
    * Maximal loads are used in the [Instructor Scheduling](instructor-scheduling.md) and edited on the [Instructor Assignment Preferences](instructor-assignment-preferences) page
    * This column is only displayed when there is at least one instructor in the department with a teaching preference set

* **Instructor Attributes**
    * List of attributes that the instructor has set
    * Attributes are used in the [Instructor Scheduling](instructor-scheduling.md) and edited on the [Instructor Assignment Preferences](instructor-assignment-preferences) page 
    * There is a column for each attribute type

* **Class Assignments**
    * Indicates which classes this instructor has been assigned to for the semester that is being timetabled
    * To make changes in this assignment, you need to go to the [Assign Instructors](assign-instructors) or [Edit Class](edit-class) screen (you can get there, e.g., from the [Instructional Offerings](instructional-offerings) screen) - you CANNOT assign classes to an instructor in any instructor-related screen
    * Conflicts are checked for classes displayed in bold letters

* **Exam Assignments**
    * Names of examinations assigned to an instructor
    * Final examinations are in bold

* **Ignore Too Far**
    * By default (when unchecked), the solver prohibits placement of back-to-back classes taught by the same instructor in rooms that are more than a short distance apart
    * If checked, the solver will strongly discourage but not prohibit long distances between back-to-back classes of this instructor
        * Use with caution!
        * When your timetable is created, make sure you check whether the instructor for whom you chose to ignore too far distances has a feasible timetable (that the instructor can teach back-to-back classes)
    * This check about distances will be performed only for those classes for which the instructor has the conflict checking on

* **Survey Submitted** 
    * When [Instructor Surveys](instructor-survey) are used, indicate whether the instructor has the survey already submitted
        * Shows *Not Filled*{:style='color:red;'} when the survey has not been filled
        * Shows *Not Submitted*{:style='color:orange;'} when the survey has been filled in but not yet submitted
        * Shows the date and time when the survey has been submitted

You can sort by any column, which is indicated when you roll the mouse over its header. An arrow will be displayed next to the column header to indicate by which column and in which order the list of instructors is sorted.

## Operations

* **Manage Instructor List** (Alt+M)
    * Go to the [Manage Instructor List](manage-instructor-list) screen, which allows you to import staff members or remove instructors from your list

* **Add New Instructor** (Alt+A)
    * Go to the [Add Instructor](add-instructor) screen to add a new instructor
