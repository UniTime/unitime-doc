---
layout: default
title: Departments
---


## Screen Description

The Departments screen contains a list of departments. Click on any department to edit its details.

![Departments](images/departments-1.png){:class='screenshot'}

## Details

The top line contains the session for which the list is valid. You can change the session from the [Academic Sessions](academic-sessions) screen.

The list of departments consists of the following columns:

* **Code**
    * The departmental number (maybe the departmental ID within the university)
    * Used in imports/exports (corresponds to the "department" element in the XML staff file)

* **Abbreviation**
    * Abbreviation of the department

* **Name**
    * Name of the department

* **External Manager**
    * The abbreviation of the external manager if the department externally manages classes

* **Subjects**
    * Number of [subject areas](subject-area) associated with the department

* **Rooms**
    * Number of [rooms](rooms) available to this department for timetabling

* **Status**
    * Status of the department (see possible values in the description of the [Edit Department](edit-department) screen)
    * The department statuses can be used to control access for a particular department, providing a finer level of control than the academic session status.

* **Distribution Preference Priority**
    * A distribution preference set up between different departments is applied to the department with the highest number
    * This priority should correspond with the order in which the problems are being solved (e.g., large rooms first, then all departmental problems, then computing labs)

* **Allow Required**
    * By default, the departmental schedule managers of regular departments cannot use required/prohibited when setting preferences for the classes managed by an external manager
    * "Required/Prohibited" can be allowed for time preferences, room preferences, distribution preferences, or all in the [Edit Department](edit-department) screen
        * If this "Required/Prohibited" property is set on a department that is marked as an external manager, anyone who is allowed to change a class can set required/prohibited preferences on it.
        * If the property is set on a department that is not marked as an external manager, managers from that department can put required/prohibited preferences on any externally managed classes from their subject area(s).
    * The column contains the possible values: **Time**, **Room**, **Distribution**, a combination of these, or **All** when all required/prohibited preferences are allowed

* **Instructor Preferences**
    * If checked, instructor preferences should be automatically carried over to classes.
    * Required/prohibited preferences set on the instructor may be weakened (to strongly preferred/discouraged) when required/prohibited preferences are not allowed
    * If not checked, the instructor preferences can be copied over from the instructor to the class on the [Edit Class](edit-class) screen (when the instructor is being added onto/removed from the class using the [Edit Class](edit-class) screen)

* **Events**
    * If checked, event management is enabled for this department.

* **Student Scheduling**
    * If checked, courses of this department should be included in student scheduling.

* **External Funding Dept**
    * If checked, the department can be used as an External Funding Department for classes.
    * This column is not visible by default.  To enable this column, the `unitime.courses.funding_departments_enabled` application property must be set to true in the [Application Configuration](application-configuration)

* **Last Change**
    * Date and name of the user who made the last change to the input data associated with this department

**Note:** Check the **Show all departments (including departments with no manager and no subject area)** to display all departments. By default, this is unchecked so that only departments that have some subject areas (and so timetabling can be done for them) are displayed

## Operations

* **Add Department** (ALT+D)
    * Add a [new department](add-department) to the list

* **Export PDF** (ALT+P)
    * Export the list of departments into a PDF document

