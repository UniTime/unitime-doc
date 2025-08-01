---
layout: default
title: Date Patterns
---


## Screen Description

The Date Patterns screen contains a list of date patterns for a given academic session.
 
![Date Patterns](images/date-patterns-1.png){:class='screenshot'}

A date pattern defines a set of dates associated with a term when a class may meet. The actual meeting times of a class are computed as a projection of a time pattern onto a date pattern (e.g., a class that is taught on Tuesdays and Thursdays meets on all dates from the date pattern that are on Tuesday and Thursday). Normally, a date pattern should contain all dates of particular weeks (e.g, Week 1-4 contains all dates between Monday of the first week and Sunday of the 4th week). Date patterns consist of dates rather than weeks in order to allow institutions to shift weeks around holidays.

## Details

The list of date patterns contains the following information:

* **Name**
    * Name of the date pattern

* **Type**
    * Type of the date pattern (**Standard**, **Alternate Weeks**, **Non-Standard**, **Extended**)
    * These types may be helpful for organizing the list of date patterns.
        * On classes and scheduling subparts, date patterns are ordered based on these types (Standard date patterns first, then Alternate Weeks, etc.)
    * If the type is **Extended**, only explicitly indicated departments (and administrators) have access to this date pattern (these are not visible as options on classes and scheduling subparts that are managed by departments not listed on these date patterns)
    * The **Alternative Pattern Set** is a special type. It does not have individual dates, but it contains one or more other date patterns that are alternatives to each other. When used, this allows the solver to pick one of the alternative date patterns for the class.

* **Used**
    * Checked if the date pattern is being used for some class
    * Please note that it is not allowed to delete a date pattern if it is being used

* **Weeks**
    * Number of weeks the Date Pattern spans

* **Dates / Patterns**
    * Dates that constitute this date pattern (for normal date patterns)
    * Alternative date patterns for the **Alternative Pattern Set** date pattern

* **Departments**
    * Departments that have access to this date pattern if the date pattern is of type **Extended**
    * If the type is not **Extended** and the date pattern is visible, all departments have access to it
    * **Alternative Pattern Set** date patterns are visible to all departments, except for the case when they have one or more departments associated with them. In this case, only the listed departments can use the date pattern.

The date patterns not usable for a given academic session are in gray letters (to make a date pattern not usable, click on it and untoggle the option visible). Such date patterns can still be used on scheduling subparts and classes that already have them, but they cannot be added to a new scheduling subpart or class. In other words, invisible date patterns are not listed in the list of available date patterns on the [Edit Scheduling Subpart](edit-scheduling-subpart), [Edit Class](edit-class), and other relevant classes except for the case when they are already used for the subpart/class.

## Operations

Click on a date pattern to edit or delete a date pattern using the [Edit Date Pattern](edit-date-pattern) screen.

* **Add Date Pattern**
    * Add a new date pattern in the [Add Date Pattern](add-date-pattern) screen

* **Assign Departments**
    * After a roll forward of an academic session, find classes that have an extended date pattern and authorize the departments of these classes to use these date patterns

* **Push Up**
    * After a roll forward of an academic session, if preferences were rolled forward on the class level, for each scheduling subpart that has all classes with the same date pattern, apply the date pattern push the date pattern up to the scheduling subpart

* **Export CSV**
    * Export the list of date patterns into a CSV file that can be easily opened in Excel

