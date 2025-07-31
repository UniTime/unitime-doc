---
layout: default
title: Timetable Managers
---


## Screen Description

The Timetable Managers screen contains a list of all users allowed to work with the timetabling application (all managers). The list can be sorted by any column. Click on any manager to make changes.

![Timetable Managers](images/timetable-managers-1.png){:class='screenshot'}

## Details

The columns in the list are as follows

* **Roles**
	* The default manager roles are:
		* **System Administrator** - user who has access to all screens and can do anything
		* **Session Administrator** - user who has access everything related to the academic session(s) they are associated with (through their department)
		* **Departmental Schedule Manager** - user who has access to and can change the input course timetabling and examination data of certain department(s)
		* **Curriculum Manager** - user who has access to and can change the curricula for their department
		* **Examination Timetabling Manager** - user who has access to and can change and timetable examinations for the academic session of their department
		* **Event Manager** - user who can approve or reject events for rooms in their department
		* **View All User** - user who has access to the (timetabling) data of all departmental schedule managers but cannot make any changes
	* Additional roles can be defined on the [Roles](roles) page and their permissions on the [Permissions](permissions) page

* **External ID**
	* Manager's (user's) ID
	* Must match the external ID of the authenticated user (e.g., through the [Users](users-database-authentication) page or [CAS](CAS) authentication)

* **Name**
	* User's last and first name and middle initials

* **Email Address**
	* User's email address

* **Department**
	* Department number and abbreviation of departments associated with the manager

* **Subject Area**
	* Subject areas associated with the manager's departments

* **Solver Group**
	* Solver group(s) for which the manager can do timetabling (run the solver etc.)

* **Last Change**
	* Last change made by the manager

Click on a line with a manager to change the values in any of the columns.

## Notes

Please note that all information except of the solver groups and departments are session-independent (there is one record for each timetabling manager shared between all the academic session). This means that a user cannot have a different role for different academic sessions or departments, but they may be associated with different departments or solver groups in each academic session.

By default, only managers that have at least one department from the current academic session associated with them are shown. Check the **Show all managers** checkbox to show all managers, including those that have no department from this academic session (and therefore no access except if they have a session-independent role such as System Administrator).

## Operations

* Click on a manager to go to the [Edit Timetable Manager](edit-timetable-manager) screen

* **Add Timetable Manager** (ALT+T)
	* Go to the [Add Timetable Manager](add-timetable-manager) screen to add a new manager

* **Export PDF/CSV**
	* Export the list of managers to a PDF or a CSV document
