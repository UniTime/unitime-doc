---
layout: default
title: Add Reservation
---


## Screen Description

The Add Reservation screen allows the user to add a new reservation.

## Details

* **Instructional Offering**
	* Instructional offering on which the reservation should be made
	* To look up an instructional offering by its subject area, course number, or name, click on the magnifying glass next to the text field to get to the [Course Finder](course-finder) screen

* **Reserved Space**
	* Number of spaces that should be reserved through this reservation
	* Can be edited only for Curriculum reservation
		* There is a grey text in italics under the text box indicating limits on the number of reserved spaces that arise from the restrictions or e.g. from the expected number of students in a curriculum - this text is displayed only if there may be a conflict between the reserved spaces and other limits
	* Calculated automatically for Individual reservations (= how many students are in the list of students)
	* Depends on the course limit in Course reservations

* **Expiration Date**
	* Date upon which the reservation expires, i.e., the reserved spaces are made available for other students
	* The format is MM/DD/YYYY
	* Click on the calendar icon next to the text field to be able to pick a date from the calendar
	* If no expiration date is set, the reservation does not expire

* **Restrictions**
	* Restrictions within the instructional offering regarding which part(s) of the instructional offering the reservation is set on
		* Click on the plus sign in front of a configuration to unfold its structure; you may need to click more plus signs to unfold it further

* **Type**
	* Further parameters are based on the type of reservation selected in the drop down list
		* Individual Reservations
			* Students
				* An individual reservation will be created for each of the students in the list
				* Click on the **Lookup** button to look up students in the Students table in the database through the [People Lookup](people-lookup) screen
				* You can also copy/paste a list of External Ids into the list of students (instead of looking them up individually)
		* Student Group Reservations
			* Student Group
				* Student group for which the reservation should be made
				* Student groups can be set up through Administration -> Student Groups
		* Curriculum Reservations
			* Curriculum
				* It is possible to import Curricula via an XML or enter/edit them manually in Courses -> Curricula
				* It is also possible to enter a curriculum reservation without setting up curricula in UniTime - only select academic area, classification & major(s)
			* Academic Area
				* Academic area for which the reservation should be made
			* Classifications
				* Year(s) or semester(s) of study
			* Majors
				* One or more majors within the selected academic area
		* Course Reservations
			* Course
				* A course within the instructional offering for which the reservation should be made
				* Helpful for cross-listed courses

## Operations

* **Save**
	* Save the new reservation and go back to the [Reservations](reservations) screen

* **Back**
	* Go back to the [Reservations](reservations) screen without saving any changes
