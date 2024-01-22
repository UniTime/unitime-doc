---
layout: default
title: Edit Student Group Type
---


## Screen Description


 The Edit Student Group Type page allows to modify an existing student group type. This way, student groups can be grouped by their type. There are additional properties that can be defined for each group of a particular type.

## Details


 Each student group type can have a code, a name, and the following properties:

* **Keep Students Together**
	* When set to true, the student scheduling solver will try to keep students of such groups together.

* **Disabled Sections**
	* It is possible for certain student groups to allow students to enroll in classes that are disabled for student scheduling. The possible values are:
	* **Not Allowed**: students of such group are not allowed to see or enroll in disabled classes (this is the default)
	* **Allowed With Group Reservation**: students of such a group can enroll in a disabled class if there is a student group reservation for their group
	* **Allways Allowed**: students of such a group can enroll in any disabled class

* **Advisors Can Set**
	* Advisors and admins can use the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard) to add or remove a student from a group of this type

## Operations

* **Save**
	* Save the modified student group type and go back to the [Student Group Types](student-group-types) screen

* **Delete**
	* Delete the selected student group type and go back to the [Student Group Types](student-group-types) screen

* **Previous / Next**
	* Save the modified student group type and go to the Edit Student Group Type screen for the previous / next student group type

* **Back**
	* Go back to the [Student Group Types](student-group-types) screen without saving this new status type


![Edit Student Group Type](images/edit-student-group-type-1.png){:class='screenshot'}
