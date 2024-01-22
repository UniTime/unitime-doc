---
layout: default
title: Student Sectioning Dashboard
---


## Screen Description


 The Student Sectioning Dashboard screen displays information about student requests/enrollments that have been loaded into the batch sectioning solver. There are numerous filtering capabilities on this page.

## Details

### Filter

* Hold your mouse over the text field for two seconds to see possible filtering parameters and their required format, same as described below

* Filter course enrollments or wait-listed course requests by any word from the course name or title. You can also use the following tags
	* area: academic area abbreviation
	* classification: academic classification code
	* consent: offering consent
	* course: course offering name
	* department: course controlling department code or abbreviation
	* group: student group abbreviation
	* major: academic major code
	* reserved: enrollments with a reservation
	* student: student name or external id
	* subject: subject area abbreviation
	* waitlist: wait-listed course requests
	* status: student scheduling status
	* Note that when you enter a tag, a drop down list of options for that tag will be displayed - especially when you start typing

* Use or, and, not, and brackets to build a boolean query.

* Example: subject:AAE and (waitlist:true or consent:waiting)

* Click **Search** to apply the filter

### Table(s)


 The table has two tabs on top - Enrollments and Students. A different table is displayed for each of them. Keep in mind that the table reflects the restrictions entered in the Filter.


 **Enrollments**


 The top line of the column headers refers to courses, the bottom line to classes.

* A column with clickable plus signs that enable unfolding of a course into lines with individual classes

* **Subject / Type**
	* Subject area on the line with a course
	* Instructional Type on the line with a class

* **Course / External Id**
	* Course number on the line with a course
	* External Id or the section number of a class on the line with a class

* **Title / Time**
	* Course title on the line with a course
	* Assigned time of a class

* **Date**
	* Dates during which the class is taught

* **Consent / Room**
	* Type of required consent for a course (if empty, no consent is required)
	* Room where a class is taught

* **Available**
	* Total number of available seats / total number of seats

* **Projection**
	* Total number of projected students for the course or class

* **Enrollment**
	* Number of students enrolled into the course or class (filtered by filtering criteria)

* **Wait-Listed**
	* Number of students who have been wait-listed for the course or class (filtered by filtering criteria)

* **Reservation**
	* Number of students enrolled into the course or class via a reservation (filtered by filtering criteria)

* **Need Consent**
	* Number of students who need consent to be able to take the course (filtered by filtering criteria)


 The table can be sorted by any table header - just click on it, then on the "Sort by" option that opens.


 Click on any line to get to the [Enrollments](enrollments-of-class-or-course) pop-up window with a list of enrolled students for a given course or class.


 **Students**


 The table of students lists students that meet the criteria of the Filter (e.g., all students who take a course from a given subject area, or all students of a given major, etc.).

* **Student**
	* Name of the student

* **Area**
	* Academic area

* **Clasf**
	* Academic classification

* **Major**
	* Student's major

* **Group**
	* Student group to which the student belongs

* **Status**
	* Sectioning status of the student (if there is nothing in that column, the student can be sectioned)

* **Enrollment**
	* Number of courses into which the student is enrolled

* **Wait-Listed**
	* Number of courses for which the student is on a wait list

* **Reservation**
	* Number of courses into which the student has been enrolled via a reservation

* **Consent**
	* Number of courses into which the student is enrolled that require consent

* **Requested**
	* Date and time when the student made his/her requests for courses


 Click on any line from the table to get to a list of [Classes](classes-for-student) for a given student.


 The table ends with a line of totals for number of students, student enrollments, wait listed student requests, reservations, and required consents.

## Operations

* **Search**
	* Apply the search criteria from the Filter
