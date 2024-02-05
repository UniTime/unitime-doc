---
layout: default
title: Edit Reservation
---


## Screen Description

The Edit Reservation screen allows the user to edit an existing reservation.

## Details

* **Instructional Offering**
	* Instructional offering on which the reservation should be made
	* Not editable in this screen

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
	* Further parameters are based on the type of reservation (the type is not editable in this screen)
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
			* Note: It is possible to enter a curriculum reservation without setting up curricula in UniTime - only select academic area, classification & major(s)
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
	* Save the new reservation and go back to the previous screen

* **Delete**
	* Delete this reservation and go back to the previous screen

* **Back**
	* Go back to the previous screen without saving any changes

## Notes

There is a difference between setting an expiration date on a reservation and deleting a reservation. When a reservation is deleted, UniTime does not know about it any more. When a reservation has expired, UniTime knows about it and still sections/schedules the students into their correct sections; only the not yet occupied seats are available for any other students. This is useful for example when students have individual reservations and allow overlaps of their classes. If such an individual reservation is deleted (instead of "just" expired), there is a conflict between overlapping classes and it is not possible for that student to be scheduled into both of them.
