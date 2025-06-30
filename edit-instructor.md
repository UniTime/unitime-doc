---
layout: default
title: Edit Instructor
---


## Screen Description

Edit information about an instructor in this Edit Instructor screen.

![Edit Instructor](images/edit-instructor-1.png){:class='screenshot'}

## Details

* **External Id**
	* Id that identifies this instructor throughout UniTime
	* If possible, matches the university's employee Id

* **Account Name**
	* If you know the university account name of a new instructor, you can look the person up by this account
	* **Note:** This field is user maintained and is not required elsewhere in UniTime

* **First Name**
	* First name of the instructor
	
* **Middle Name**
	* Middle name of the instructor

* **Last Name**
	* Last name of the instructor
	* The only mandatory field in this screen

* **Last Name**
	* Academic title of the instructor (optional)

* **Email**
	* Instructor's email address

* **Department**
	* Shows the department selected in the [Instructors](instructors) screen

* **Position**
	* Position classification of this instructor
	* **Note:** This field is user maintained and is not required elsewhere in UniTime; it may be useful, however, for grouping instructors or in exports for departmental report

* **Notes**
	* For your use only

* **Ignore Too Far**
	* By default (when unchecked), the solver prohibits placement of back to back classes taught by the same instructor in rooms that are more than a short distance apart
	* If checked, the solver will strongly discourage but not prohibit long distances between back to back classes of this instructor
		* Use with caution!
		* When your timetable is created, make sure you check whether the instructor for whom you chose to ignore too far distances has a feasible timetable (that the instructor can in fact teach the classes that are back to back)

## Operations

* **Update** (Alt+U)
	* Save changes and return to the [Instructor Detail](instructor-detail) screen

* **Delete** (Alt+D)
	* Delete this instructor from the list of instructors
		* Takes you back to the [Instructors](instructors) screen
		* Note: The button is displayed only when there is no class or examination associated with this instructor

* **Lookup** (Alt+L)
	* Look up this instructor's External Id (and other related information) using the [People Lookup](people-lookup) dialog

* **Previous** (Alt+P)
	* Save changes and go to the Edit Instructor screen for the previous instructor in your list of instructors

* **Next** (Alt+N)
	* Save changes and go to the Edit Instructor screen for the next instructor in your list of instructors

* **Back** (Alt+B)
	* Return to the [Instructor Detail](instructor-detail) screen without saving any changes
