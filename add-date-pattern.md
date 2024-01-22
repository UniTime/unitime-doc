---
layout: default
title: Add Date Pattern
---


## Screen Description


 The Add Date Pattern screen provides interface for adding a new date pattern.


 A date pattern defines a set of dates associated with a term when a class may meet. The actual meeting times of a class are computed as a projection of a time pattern onto a date pattern (e.g., a class that is taught on Tuesdays and Thursdays meets on all dates from the date pattern that are on Tuesday and Thursday). Normally, a date pattern should contain all dates of particular weeks (e.g, Week 1-4 contains all dates between Monday of the first week and Sunday of the 4th week). Date patterns consist of dates rather than weeks in order to allow institutions to shift weeks around holidays.

## Details

* **Name**
	* Name of the date pattern

* **Type**
	* Type of the date pattern (Standard, Alternate Weeks, Non-Standard, Extended)
		* These types may be helpful for organizing the list of date patterns
			* On classes and scheduling subparts, date patterns are ordered based on these types (Standard date patterns first, then Alternate Weeks, etc.)
		* If the type is Extended, only explicitly indicated departments (and administrators) have access to this date pattern (these are not visible as options on classes and scheduling subparts that are managed by departments not listed on these date patterns)

* **Visible**
	* When checked (checked by default), the date pattern will be available to users authorized to use it
	* When not checked, the date pattern will not be available for the given academic session and will be displayed in gray letters in the list of date patterns; if the date pattern was used before it was made invisible, it will stay on a class but it will no longer be an option to pick on other classes

* **Default**
	* Checked if this date pattern is the default date pattern for all classes
	* The default date pattern is displayed in bold letters in the list of date patterns
	* To change the default date pattern, go to the add/edit screen of the date pattern that should be default and click on the Make Default button (alternatively, you can select a default date pattern on [Edit Academic Session](edit-academic-session) screen)

* **Departments**
	* For the date patterns of type Extended, it is necessary to specify which departments should have access to the date pattern (unless the date pattern should be used by administrator only)
	* Select a department in the drop down menu and click **Add Department** to authorize the department to use the date pattern (not applied until Save is clicked)
	* Select a department in the drop down menu and click **Remove Department** to withhold the authorization to use a given date pattern by that department

* **Pattern**
	* Indicate days of instructions in the calendar

## Operations

* **Save**
	* Save the date pattern and go back to the list view

* **Make Default**
	* Save changes, make the date pattern the default date pattern and go back to the list view

* **Back**
	* Go back to the list view without saving anything


![Add Date Pattern](images/add-date-pattern-1.png){:class='screenshot'}
