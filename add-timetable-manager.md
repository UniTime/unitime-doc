---
layout: default
title: Add Timetable Manager
---


## Screen Description

In the Add Timetable Manager screen you can add a new user and indicate which departments should be associated with him/her.

![Add Timetable Manager](images/add-timetable-manager-1.png){:class='screenshot'}

## Details

There are two different layouts of the upper part of the screen, in one case all users are entered through the timetabling application (users are authenticated by the application), in the other case the application is connected to an employee database (users are authenticated through an external interface).

### Using Internal Authentication

The upper part of the screen contains the following

* **Academic Session**
	* Session to which the new user should have access
	* Can be changed from the [Academic Sessions](academic-sessions) screen

* **First Name**

* **Middle Name**

* **Last Name**

* **External ID**
	* Assign an ID number to the user (the ID must be the same as the External ID in the [Users (Database Authentication)](https://sites.google.com/a/unitime.org/help/Users_%28Database_Authentication%29) screen)

* **Email Address**
	* Enter contact email address

### Using External Authentication

The upper part of the screen contains the following

* **Academic Session**
	* Session to which the new user should have access
	* Can be changed from the [Academic Sessions](academic-sessions) screen

* **External ID**
	* ID that can be looked up in e.g. an employee database
	* Click on **Lookup Manager** to fill in the rest of user information (such as email address) based on his/her external ID - the name of the user will be displayed above the top line of this screen

* **Email address**
	* New user's email address

* **External Manager**
	* Indicates whether the user is associated with a department that is marked as an external manager, see [Edit Department](edit-department) for more details.

### Departments

Select a department in the drop down list and click **Add Department** to make the user a manager for a department. Add as many departments as needed.

Note: A user that has "Departmental Schedule Manager" role has to be associated with at least one department.

### Solver Groups

Select a solver group for which the user should be able to create a timetable and click **Add Solver Group**. Do it for all solver groups to which the user should have access.

### Roles

Select a role for the user from the drop down list and click **Add Role**. Add as many roles as needed and then select which one of them should be the primary role (the one applied whenever the user logs on to the application).

Note: Only the "Departmental Schedule Manager" role reflects the choice of departments and solver groups in this screen. "View All" and "Administrator" have access to all data (a user in the "View All" role cannot make any changes and can only see committed timetables).

Note: A user needs to be associated with at least one role.

## Operations

* **Save** (Alt+S)
	* Save this new user and go back to the [Timetable Managers](timetable-managers) screen

* **Back** (Alt+B)
	* Go back to the [Timetable Managers](timetable-managers) screen without saving this new user


