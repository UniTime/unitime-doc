---
layout: default
title: Student Scheduling Assistant
---


## Screen Description

The Student Scheduling Assistant helps students build a workable class schedule.  It takes a list of courses a student is interested in and determines the class sections the student needs to take in order to get as many of the courses being requested as possible.  The Student Scheduling Assistant tries to calculate a schedule for the student based on the following criteria:


* the student’s priority for the course
* the student’s free time requests
* the student must be able to attend all parts of the course
* provide as many of the selected courses as possible
* the distance between back-to-back classes (if distance between two classes is greater than a normal person can cover during the break time a roadrunner icon is displayed)
* whether an overlap is allowed between two classes
* keep existing schedule as much as possible
* substitute courses are only used if a selected course is not available
* a section choice that prevents the fewest future students from also getting the course

Once the assistant has suggested a schedule a student can make changes to the schedule until she finds a combination of time for the classes that meets her needs.

Additional information is available in the [Student Scheduling Assistant Manual](manuals/scheduling-assistant).

In the Student Scheduling Assistant screen, a student may enter a prioritized list of courses he/she would like to take in a given term. It is also possible to enter course alternatives and free time requests. Then a personal schedule is offered to the student and he/she can enroll in the classes as offered.

![Student Scheduling Assistant](images/student-scheduling-assistant-1.png){:class='screenshot'}


## Courses and Priorities

The student begins with the screen in this mode to set up a list of prioritized courses with alternatives and free time requests.

### Course Requests

Table of courses ordered by student's priority (courses on the first line have the highest priority). Each course can have one or more alternatives that have the same priority for the student as his/her first choice on a given line. The second or later choice are only used if the first choice is unavailable or does not fit with higher priority courses in the list.

Click on the magnifying glass ![Course Finder](images/icon-finder.png) icon to get to the [Course Finder](student-course-finder) screen for more information about possible courses.

If at least one alternative course is provided, click the swap ![Course Swap](images/icon-swap.png) icon to swap the course with its alternative.

Click the plus ![Add](images/icon-filter-add.png) icon to add an additional alternative.

Click the times ![Clear](images/icon-filter-clear.png) icon to clear the course.

If the wait-listing is available, and the selected course can be wait-listed, the Wait-List checkbox will appear. If the student cannot be enrolled in a course with the Wait-List toggle checked, they will be automatically put on a wait-list for the course.

To move a line with a course and its alternatives one line up or one line down, click on the appropriate arrow ![Up](images/icon-button-up.png) ![Down](images/icon-button-down.png) at the end of the line. To remove the whole line, click the trash bin ![Delete](images/icon-button-delete.png) icon.


### Substitute Course Requests

Table of substitute courses in the order of priority. These alternatives will be used if some of the courses from the Courses table and their alternatives cannot be scheduled (due to conflicts with higher priority courses or because they are full already).

### Operations

* **Preferences**
	* Additional preferences that apply to all the requested courses

		![Student Scheduling Assistant](images/student-scheduling-assistant-5.png)

	* Prefer face-to-face or online courses
	* Prefer or discourage back-to-back classes
	* When enabled (typically for Summer terms), it is also possible to
		* require online courses, or
		* set start/end dates for the classes (only classes offered between the selected dates would be available)

* **Advisor Recommendations**
	* Display the advisor course recommendations when available

* **Current Registration**
	* Discard all changes and reset the page back to the current registration

* **Build Schedule**
	* Run the scheduling assistant, then display the resulting timetable

## Personal Schedule

The Personal Schedule mode of the Student Scheduling Assistant screen presents a list of classes with their assigned times and rooms to which further changes can be made. The user can click on any class and get to the [Alternatives](alternatives-for-class) screen where there are options for change (if any change is possible) - for example, to take a course at a different time or in a different location.

![Student Scheduling Assistant](images/student-scheduling-assistant-2.png){:class='screenshot'}

### List of Classes

* **Lock**
	* When checked, the class cannot be changed in the [Alternatives](alternatives-for-class) screen - the changes that would include the class are not even displayed

* **Subject**
	* Subject area of the class

* **Course**
	* Course that contains the class

* **Type**
	* Type of class (Lecture, Recitation, ...)

* **Class**
	* Identification of the class

* **Avail**
	* Number of free, still available seats / capacity of the class 
	* Negative number means that the class is overbooked

* **Days**
	* Days of the week

* **Start**
	* Start time of the class

* **End**
	* End time of the class

* **Date**
	* Dates during the semester on which the class is taught

* **Room**
	* Room where the class meets
	* If there is a road runner icon ![](images/icon-distance.png), it means that the room is far from the previous class; roll the mouse over the icon to see the distance to travel from the room of the previous class to here
	* Long distances, typically between two campuses, are indicated by a race car icon ![](images/icon-long-distance.png)

* **Instructor**
	* Instructor for the class
	* Click on the envelope icon to send an email to the instructor (if there is no icon, the email address is not available)

* **Requires**
	* Identification of other classes from the List of Classes that are required to be taken together with this class (for example, a specific lecture may be required for a given recitation)

* **Note**
	* Consent, if a departmental or instructor consent is required.
	* Course schedule of classes note, if present
	* Class schedule note, if present

* **Credit**
	* Number of credits

* **Status Icons**
	* ![](images/icon-tick.png) **Green checkmark:** You are currently registered for the given class.
	* ![](images/icon-delete.png) **Red cross:** You are currently registered for the given class. This enrollment will get dropped when Submit Schedule button is clicked.
	* ![](images/icon-add.png) **Green plus:** You are currently not registered for the given class. Please click the Submit Schedule button to update your registration.
	* ![](images/icon-problem.png) **Red circle exclamation mark:** Registration for the given class has failed. The appropriate error message is in the tool tip.
	* ![](images/icon-error.png) **Yellow triangle exclamation mark:** Course of the given class is currently undergoing maintenance / changes.
	* ![](images/icon-overlap.png) **Two overlapping rectangles:** Given class is overlapping with some other class. If classes are allowed to overlap, the overlapping time is minimised instead.
	* ![](images/icon-group.png) **Two people icon:** There are more students expected than seats available; please, try to avoid this class if possible. To see if another class is available, click on the class; that will take you to the [Alternatives](alternatives-for-class) screen.
	* ![](images/icon-stop.png) **Red circle cross:** The class has been cancelled. 

Click on any class in the list to get to the [Alternatives](alternatives-for-class) screen to see if there are alternative times or rooms for that class.

There is a small toggle **Show unassignments** in the lower right-hand corner. When the checkbox is checked, any classes that would be unassigned as a result of the current work with the Student Scheduling Assistant will be displayed.

### Time Grid

Student's schedule displayed as a time grid (as opposed to a list of classes).Click on any class in the timetable to get to the [Alternatives](alternatives-for-class) screen to see if there are alternative times or rooms for that class.

![Student Scheduling Assistant](images/student-scheduling-assistant-4.png){:class='screenshot'}

### Student Availability

A student may not be available during a particular time because he/she is teaching some other class. Both batch and online solvers now consider this student/instructor availability. A student can now see his/her teaching assignments in the Scheduling Assistant as well.

![Student Scheduling Assistant](images/student-scheduling-assistant-3.png){:class='screenshot'}

Teaching assignments are on top of the list, in dark blue with the teacher icon ![](images/icon-teacher.png). The teacher icon is not present when the student must be available during the class, but is not assigned as an instructor to it -- see [Instructor Scheduling](instructor-scheduling) component, common classes.

## Operations

* **Add/Drop Courses** 
	* Go back to the list of prioritized courses and course alternatives

* **Rearrange Schedule**
	* Reschedule the requested courses all over again (as opposed to just adding a new course with as few changes as possible, which happens when a course is added to the prioritized list in the previous screen)

* **Current Registration**
	* Discard all changes and reset the page back to the current registration

* **Submit Schedule**
	* Enroll the student in the classes displayed in the List of Classes or in the Timetable
	* This option is available when Online Sectioning is enabled for the academic session

* **Print**
	* Print out the Timetable and the List of Classes

* **Export** (if enabled)
	* Export the timetable as an iCalendar file

* **![](images/icon-add.png) New Course** (in the bottom right corner of the List of Classes tab)
	* Quickly add a new course to the current schedule without going back to the Course Requests table. When clicked a [Course Finder](student-course-finder) dialog appears. When a course is selected:
		* If the course is already present in the Course Requests table, the user if given the choice to drop the course (remove it from the schedule).
			* If a new course is selected, [Alternatives](alternatives-for-class) dialog shows up with possible choices (if there are any). The course is only added to the schedule when a choice is selected.

## Notes

**Free time requests**

There are two ways to enter a free time request

1. In the list of courses, enter the request in the form of "Free F 10:00a - 10:30a" or "Free TR 2:00p - 3:00p" etc.
2. Go to the [Course Finder](student-course-finder) screen and click on the "Free Time" tab; then click on the times that should stay free and then press Enter