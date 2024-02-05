---
layout: default
title: Instructional Offerings
---


## Screen Description

This screen displays all instructional offerings for the selected subject area. It is separated into two parts. The first section lists "Offered Courses" - those which will be offered in the semester being timetabled (semester is visible in the upper right hand corner under the title of the screen). The second section lists "Courses Not Offered" - courses from the course catalog which are not being offered for that semester.


![Instructional Offerings](images/instructional-offerings-1.png){:class='screenshot'}

## Details

The first part of this screen helps you define what information you want to display in the list of instructional offerings. It consists of a filter and the line where you select a subject area and can type in a course number.

* In the **Filter**, you can select what information to display about each of your instructional offerings/scheduling subparts/classes. You always need to click on the Search button to apply changes you have made to the filter. Detailed description:
	* **External Id**
		* External Id of each class (how it may be represented in other systems at the university)

* **Enrollment Information**
	* **Enrollment**
		* Before the semester begins, there is the number of students enrolled in the instructional offering in the last like semester (and the column header in the table is "Last Enrollment")
		* When enrollment numbers are known for the given semester, these numbers are published here (and the column header is changed to "Enrollment")
		* Cannot be edited in this application
	* **Projected Demand**
		* Projected demand for the instructional offering
		* Can be recalculated from curricula by a schedule deputy or a curriculum manager
	* **Limit**
		* Number of students that should be able to register for a given instructional offering or for a given class
		* The total of limits per class (set up e.g. in the [Multiple Class Setup](multiple-class-setup) screen) displayed as a limit for a scheduling subpart can exceed the course limit, however, only the number of students listed on the line with the course number can enroll

* **Snapshot Limit**
	* The limit for the instructional offering at the time the Limit an Projection Snapshot was taken.
	* The limit for the classes at the time the Limit an Projection Snapshot was taken.
	* This data is for informational use only.
	* The snapshot limit can be updated by taking a new snapshot using the [Limit and Projection Snapshot](limit-and-projection-snapshot) Page.

* **Room Ratio**
	* The ratio of the required room size to the class limit
		* Room Ratio = Room Size / Limit per Class
	* Values
		* If the column is empty for a given class, it means that the room ratio is 1 (the most common value)
		* N/A is displayed when no room is used for a class (for example, if the class has arranged hours)
		* If limit per class is 0 for a given class, then the number in the Room Ratio column determines the size of room needed for that class
		* If the class needs more than one room, the number of requested rooms is also displayed in this column

* **Manager**
	* Determines who will assign time and room to this class (for example, whether it is the Large Lecture Room manager, the departmental schedule deputy, or the Computing Lab manager)
	* The managing department also determines the set of rooms and/or times (time patterns) that you can use when you set up preferences
	* Abbreviations are displayed in this column, not the full name of the manager (roll the mouse over the abbreviation to see the full name)

* **Date/Time Information**
	* **Date Pattern**
		* Indicates which weeks during the semester the class is taught
	* **Minutes Per Week**
		* Number of minutes per week
			* For example, a typical class that meets in a 2x75 or a 3x50 pattern would have 150 minutes per week (each 50 minutes being equivalent to "an hour of instruction")
	* **Time Pattern**
		* Number of meetings per week x number of minutes per meeting

* **Preferences**
	* Preferences that will be applied for a given class or scheduling subpart

* **Instructor**
	* Name of instructor assigned to a given class
	* Style of instructor's names

* Bold: The instructor's time should be reserved for the class, there cannot be a conflicting class assigned to the same instructor (unless the other class doesn't require conflict checking)

* Not bold: The instructor can have other classes that overlap with this class, conflicts are not checked

* Italics: Instructors whose names should not be displayed in the online schedule (e.g., at Purdue)

* To change the instructor for a given class, either go to its [Edit Class](edit-class) screen or go to the [Assign Instructors](assign-instructors) screen for a given instructional offering

* **Timetable**
	* Time and room assigned to a class during timetabling
		* Normally, a committed timetable is displayed, unless there is a different timetable selected or loaded into the solver for the given class
		* If there is a timetable loaded into the solver and a timetable selected, the loaded one is displayed
		* See documentation for [Timetables](timetables) page for more details.

* **Catalog Information**
	* **Title**
		* The long title of the course
		* To change it, go to the [Edit Course Offering](edit-course-offering) screen
	* **Offering Credit**
		* Credit for each of the courses in a given instructional offering (the credit must be the same for all the cross-listed courses)
		* To change this, go to the [Edit Course Offering](edit-course-offering) screen
	* **Subpart Credit**
		* Credit for a given scheduling subpart
		* Cannot be edited in this application
	* **Consent**
		* The type of consent (if any is required) for all the courses in a given instructional offering
		* To change this, go to the [Edit Course Offering](edit-course-offering) screen
	* **Designator Required**
		* Indicates whether a designator is required
		* To change this, go to the [Edit Course Offering](edit-course-offering) screen
	* **Schedule Print Note**
		* The course note that will be displayed in the Schedule of Classes
		* To change it, go to the [Edit Course Offering](edit-course-offering) screen

* **Note to Schedule Manager**
	* Note to the manager who assigns time and room for a given class; for example, if the class should be a part of the large lecture room manager's set of classes, the note will be for the LLR manager; if the class should be timetabled by the departmental schedule deputy, this note is to him/herself
	* The note is editable in the [Edit Class](edit-class) screen

* **Examinations**
	* Display examination name, period, and room(s) assigned to the course
	* When examinations are not yet timetabled, display examination name
	* More overview information about examinations can be found in the [Examinations](examinations) screen

* **Sort By**
	* Sort classes within an instructional offering and within scheduling subparts

* In the **Subject** field, you can select the subject area (if you only have one subject area, this field will be pre-populated for you and you cannot change it).

* You can use the **Course Number** field in several ways

* Leave it blank to see all the instructional offerings for a given subject area and click Search - this will display all the instructional offerings for that subject area

* Enter the course number of the course that you want to display and click Search - this will take you to the [Instructional Offering Detail](instructional-offering-detail) screen for that course

* Enter a "wild card", such as "1*" and click Search to display all 100 level courses. A variation on the use of the wildcard would be to enter "595*" to display 595 and all 595 suffix courses

* Enter the course number of a new course and click Add New to add a new course to your list - this will take you to the [Edit Course Offering](edit-course-offering) screen

* Click the **Search** (Alt+S) button to apply your filter and your selection of the subject area and the course number

* **Export PDF** (Alt+P) exports the list of instructional offerings into a PDF document which is then easy to save or print. The PDF document will automatically be opened in a new window unless you have pop-ups blocked in your browser. If so, click on the line at the top of the screen that says "If the pop-up window was blocked, you can follow this link to retrieve the exported file". That will open the document in your current window and you can save or print it from here (there should be a "Save a copy" and a "Print" icon in the menu at the top of the PDF document).

* **Worksheet PDF** (Alt+W) exports the list of instructional offerings into a PDF document organized in a way that used to be used at Purdue

* Click on **Add New** (Alt+A) after you fill in the course number of the new course in the **Course Number** field to add a new course. This will take you to the [Add Course Offering](add-course-offering) screen. If you enter a course number of a course that already exists, clicking on Add New will take you to the [Instructional Offering Detail](instructional-offering-detail) screen for that offering.

When the list of the instructional offerings is displayed, you can see for each instructional offering

* In the area with a light blue background:
	* A line with the course number (clicking on that takes you to the [Instructional Offering Detail](instructional-offering-detail) screen)
		* Immediately below this line the course numbers of any courses cross-listed with this one will be listed in gray letters
	* If there is more than one configuration, a line with the configuration name
	* A line for each scheduling subpart (clicking on a scheduling subpart takes you to the [Scheduling Subpart Detail](scheduling-subpart-detail) screen)

* In the area with white background:
	* A list of classes associated with the offering (clicking on a class takes you to the [Class Detail](class-detail) screen)


![Instructional Offerings](images/instructional-offerings-2.png){:class='screenshot'}
