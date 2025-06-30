---
layout: default
title: Class Detail
---


## Screen Description

The Class Detail screen offers an overview of information about a class. Most of the information is editable in the [Edit Class](edit-class) screen.

![Class Detail](images/class-detail-1.png){:class='screenshot'}

## Details

The following fields are displayed in the upper part of the screen (below the name of the class):

* **Manager**
    * Manager responsible for timetabling this class
    * Editable in the [Multiple Class Setup](multiple-class-setup) screen

* **Enrollment**
    * Number of enrolled students (if available)

* **Class Limit**
    * Number of students that should be able to register for a given class
    * Editable in the [Multiple Class Setup](multiple-class-setup) screen

* **Snapshot Limit**
    * The class limit at the time the [Limit and Projection Snapshot](limit-and-projection-snapshot) was taken.

* **Number Of Rooms**
    * Number of rooms needed for the class (usually one)
    * Editable in the [Multiple Class Setup](multiple-class-setup) screen

* **Room Ratio**
    * The ratio of the required room size to the class limit
        * Room Ratio = Room Size / Class Limit
    * In almost all cases, this should be one
    * Some exceptions to the norm
        * You need a room for fewer students than the class limit (Room Ratio is less than one)
        * You need a room for a class with zero limit. In this case, Room Ratio needs to contain the required room size
    * In parenthesis after the room ratio, you can see the minimum room capacity required for this class (for Class Limit <> 0, it is calculated as Minimum Room Capacity = Room Ratio * Class Limit; if Class Limit = 0, then Minimum Room Capacity = Room Ratio)
    * Editable in the [Multiple Class Setup](multiple-class-setup) screen

* **Attendance**
    * When there are two or more rooms required for the class
    * **Split Attendance** means that students are expected to split between the two (or more) rooms. That is the total capacity of the assigned room &times; the room ratio must be equal to or greater than the class limit.
    * **Alternative Attendance** means that all students are expected to be able to fit in any of the assigned rooms. That is, the room capacity of any assigned room &times; the room ratio must be equal to or greater than the class limit.
    * Editable in the [Multiple Class Setup](multiple-class-setup) screen

* **Funding Dept**
    * The department providing funding for this class.
    * This field is not visible by default.  To enable this field, the `unitime.courses.funding_departments_enabled` application property must be set to `true`.
    * Editable in the [Multiple Class Setup](multiple-class-setup) screen

* **Date Pattern**
    * Days/weeks throughout the semester during which this class will be taught
    * You can click on the icon of the calendar to see which dates belong to the selected date pattern
    * Editable in the [Edit Class](edit-class) screen

* **Display Instructors**
    * When checked (and it is checked by default), the instructors for this class will be displayed in the online Schedule of Classes
    * When not checked, the instructor will not be displayed in the online Schedule of Classes, and his/her name will have to be re-entered for reporting purposes
    * Editable in the [Edit Class](edit-class) screen

* **Student Scheduling**
    * When checked (and it is checked by default), the class will be available to students during student scheduling
    * When not checked, the class will be treated as with zero limit during student scheduling (only students with individual reservations will be able to get in) - the class not to be displayed is in italics wherever it is listed
    * Editable in the [Edit Class](edit-class) screen

* **Student Schedule Note**
    * The class note that will be displayed in the online Schedule of Classes
    * Editable in the [Edit Class](edit-class) screen

* **Requests / Notes**
    * Requests/Notes for the manager who will timetable this class
    * Displayed only if it is not empty

* **Instructors**
    * The following information is displayed and can be edited in the [Edit Class](edit-class) screen
        * **Name**
            * Instructor's name
        * **Share**
            * The percentage of teaching activity for this class associated with this instructor
        * **Check Conflicts**
            * When checked, the instructor's preferences are considered during departmental timetabling; also, checks are performed for this instructor to make sure there is no conflict for him/her between this class and his/her other classes (such as teaching two classes at the same time)
            * When not checked, the instructor's assignment to this class is ignored during timetabling; no conflict checking will be performed between this class and his/her other classes
        * **Responsibility**
            * When teaching responsibilities are defined, an instructor's teaching responsibility is listed here.
            * Teaching responsibilities can be defined on the [Teaching Responsibilities](teaching-responsibilities) page in the administration.

* **Last Change**
    * Information about the last change made to the class (recorded automatically when the [Edit Class](edit-class) screen is updated)

In the **Timetable** part, you see the time, room, and instructor assigned to this class (once a timetable has been created)

* Normally, a committed timetable is displayed unless there is a different timetable selected or loaded into the solver for the given class
* If there is a timetable loaded into the solver and a timetable selected, the loaded one is displayed
* See documentation for [Timetables](timetables) page for more details.

In the **Preferences**, you will see any preferences that have been set up for this class (with color coding for preference levels).

* In **Available Rooms**, you will see only those rooms that meet your preferences and are large enough for your class (the room capacity is greater than or equal to the minimum room capacity displayed in the upper part of this screen)
    * Only the first few available rooms are displayed by default; if there are more rooms available than displayed, there are three dots at the end of the list - click on the three dots (...) to see the full list of available rooms
* To change the preferences, click on the Edit Class button to get to the [Edit Class](edit-class) screen. There is also more detailed documentation for the preferences on the help page for that screen.

### Distribution Preferences
* The list of distribution preferences applicable to this class.
* Click on any line to open the [Edit Distribution Preference](edit-distribution-preference) page for any of the distributions.
    * [Instructor Detail](instructor-detail) page is opened when the distribution preference is set on an instructor.

There is one operation in the Distribution Preferences section:

* **Add Distribution Preference** (Alt+A)
    * Go to the [Distribution Preferences](distribution-preferences) screen to add a new distribution preference
        * The class will be pre-populated on that screen

### Examinations

* A list of examinations associated with this class
    * For an explanation of the column headings, please see the description of the column headings in the [Examinations](examinations) screen
    * The column **Student Conflicts** contains numbers of "Direct", ">2 a day", and "Back-To-Back" conflicts

* Click on a line with an examination to get to its [Examination Detail](examination-detail) screen

There is one operation in the Examinations section:

* **Add Examination** (Alt+X)
    * Go to the [Add Examination](add-examination) screen to add a new examination with the scheduling subpart filled in already

## Enrollments

The Enrollments section lists all students who are currently enrolled in the class.

* **Student**
    * Name of the student
* **Course**
    * If there is a cross-list, display the course that the student is requesting/enrolled into
* **Priority**
    * Course request priority (see [Student Scheduling Assistant](student-scheduling-assistant))
* **Curriculum (Area, Classification, Major)**
    * Student curriculum information (if applicable)
* **Reservation**
    * Type of the reservation through which the student got into the course (if applicable)
* **Enrollment**
    * For each scheduling subpart, the class number into which the student is enrolled.
* **Requested**
    * Date when the course request was made
* **Enrolled**
    * Date when the student was enrolled in the course


## Operations

* **Edit Class** (Alt+E)
    * Go to the [Edit Class](edit-class) screen to edit properties and preferences for the class

* **Assign** (Alt+X)
    * Go to the [Class Assignment](class-assignment) screen to change the time/room assignment for this class 
    * Since this is a tool explicitly for making changes to the committed timetables, with less functionality than [Suggestions](suggestions) in the solver section, this button is displayed only when
	* **Note:** The **Assign** button is only available when:
		* There is a committed timetable for the solver group of the managing department
		* No timetable is loaded nor selected

* **Previous** (Alt+P)
    * Go to the Class Detail screen for the previous class

* **Next** (Alt+N)
    * Go to the Class Detail screen for the next class

* **Back** (Alt+B)
    * Go to the last non-editable screen through which you got here

