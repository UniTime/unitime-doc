---
layout: default
title: Suggestions
---


## Screen Description


 The Suggestions screen provides you with information about a class, its current time and room assignment and possible alternatives. You can select any of the alternatives to change the assignment. If the selected assignment results in an unassignment of another class, you can continue by selecting an alternative assignment for the other class (for example, you place your current Lab 2 in a room at a time when there was Lab 1 and therefore Lab 1 gets unassigned; you continue by selecting an alternative assignment for Lab 1). The screen supports a "what if" scenario - you can select as many changes as you want and those changes will not be executed until you click the Assign button.

## Filter


 The first (foldable) part of the filter is for you to select what sections of the screen you want to display (check appropriate checkboxes) and to what extent (the following two items):

* **Simplified mode**
	* If unchecked, many additional columns appear in the Suggestions and Placements

* **Maximum number of suggestions/placements**
	* Specify how many suggestions or placements you would like to see in this screen


 The second part of the filter is not hidden when you fold the filter. All these items apply to the Suggestions and Placements parts of the screen and are reset each time you open Suggestions screen for a new class:

* **Allow placements**
	* For the purposes of finding an alternative time/room placement (assignment), you can select to display all possibilities (No Restriction), only possibilities that have the same time but a different room (Same Time) or only possibilities that have the same room but a different time (Same Room)

* **Text filter**
	* Enter a substring by which you want to filter the possible placements of the selected class
	* Examples:
		* Enter a building abbreviation to find placements within a building
		* Enter M to find placements with a Monday time
		* Enter 8:30 to find possible placements that cause the class to begin at 8:30

* **Room size filter**
	* Enter the range of possible room size - only placements that include a room of that size will be displayed

### Operations

* **Apply**
	* Apply changes made in the Filter section of the screen

* **Close** (Alt+C)
	* Close the window with the Suggestions screen


![Suggestions](images/suggestions-1.png){:class='screenshot'}

## Current Assignment


 Information about the current time and room assignment for a given class. If an item is not applicable for the selected class, it is not displayed (for example, the Instructor line is not displayed if there is no instructor assigned to teach this class).

* **Date**
	* Date pattern for the class

* **Time**
	* Time currently assigned to this class (includes days and time)
	* Can be changed in this screen

* **Room**
	* Room(s) currently assigned to this class
	* Can be changed in this screen

* **Instructor**
	* The instructor assigned to teach this class who requires conflict checking for this class (this assignment has to be done in the Input Data section before data is loaded into the solver)

* **Student Conflicts**
	* Number of student conflicts with other classes

* **Violated Constraints**
	* Listing of any distribution and back-to-back instructor preferences violated by this assignment

* **Room Locations**
	* Possible room placements for the class - rooms that are large enough to seat all the students from the class
		* The number before the parenthesis is the number of possible room placements
		* A list of those room placements follows in the parenthesis
			* Expand the list by clicking on the three dots at the end of the list to display all possible room placements
			* Prohibited room selections are displayed in red. Rooms that are too small are displayed with a strike-through. These are only displayed and selectable in interactive mode.

* **Time Locations**
	* Possible time placements for the class - times within selected time patterns that are not prohibited
		* The number before the parenthesis is the number of possible time placements
		* A list of those time placements follows in the parenthesis
			* Expand the list by clicking on the three dots at the end of the list to display all possible time placements
			* Prohibited time selections within allowed time patterns are displayed in red. Times from disallowed patterns are displayed with a strike-through. These are only displayed and selectable in interactive mode (i.e., a solution was loaded into the solver using [Timetables](timetables) page, or using [Solver](solver) page with Allow breaking of hard constraints toggle switched on).

* **Minimal Room Size**
	* Size of the smallest room that can be used for this class


 Color coding is employed for the information about times and rooms - see the legend under the Current Assignment section in the Suggestions screen.


![Suggestions](images/suggestions-2.png){:class='screenshot'}

## Selected/Conflicting Assignments / Selected Suggestion


 Information about the change you are about to make. If there are conflicting assignments, they are listed in the Conflicting Assignments section, together with the constraint that causes the conflict, such as room or instructor or a distribution preference. You can click on the conflicting class and find a new time/room assignment for it, which will then become a part of the selected assignment.


 If you want to make the change, click **Assign**, if not, click on the trash bin on the line with the class in the selected assignment or exit the Suggestions screen.


![Suggestions](images/suggestions-3.png){:class='screenshot'}

## Conflict Table


 This table lists possible times with the student conflicts and violated distribution preferences that will occur if the time is selected for the class. This information should help you decide what time to choose if you want to make a change in time. The underlined time is the current assigned time for the class.


 Click the three dots next to the number of Student Conflicts to see the details of those conflicts. Click the three dots next to the number in the column of Violated Distr. Constr. to see which constraint will be violated if the time on that line is selected.

## Suggestions


 This section contains a list of possible changes to the time/room assignment for the class. The Score indicates how good/bad the change is for the timetable (the lower the number the better). The table is by default sorted by Score, but it can be sorted by any column - just click on the column header.


 Click on any of the suggestions to make it your selected suggestion - then click on the Assign button to make this change happen.


 Note: You can work with the Filter in the upper part of this screen to look for suggestions that include only a specific time or a specific room.


![Suggestions](images/suggestions-4.png){:class='screenshot'}

## Placements


 Displays all allowable placements for this class.


 The difference between Suggestions and Placements is that Suggestions do not leave classes unassigned - the changes suggested there include alternative assignments for classes that would be left unassigned in Placements.

## Conflict-based Statistics


 The conflict-based statistics are a record of the conflicts created during the solver's attempts to assign possible rooms and times to the class (i.e., other class assignments that were incompatible) and the reasons for these conflicts. These reasons correspond to violations of various constraints on the problem (for example, two classes requiring a single instructor at the same time, or three classes requiring the same time when only two rooms are available). Typically these conflicts are caused by too many classes competing over a fixed resource. The statistics can help point out the constraining resource, or an overly restrictive requirement, so that changes can be made to the input data which allow the problem to be solved.


 Each line in the conflict-based statistics table contains a number indicating how many times a conflict occurred and the constraint that was in contention. Clicking on the small plus sign at the beginning of the line will provide an expanded breakdown of the conflicts for this constraint. Continue opening lines with large numbers of conflicts until you have a line with a small dot rather than a plus sign. These lines indicate the classes with which your unassigned class was competing over a constraint.


 Conflict-based statistics are only displayed after the solver has been executed (they are not displayed if the timetable has only been loaded into the solver).


 Usage: It is helpful to look at the conflict-based statistics for the classes that are in the [Not-Assigned Classes](not-assigned-classes) screen to find out about problems you can fix in the input data (so that the next time you run the solver, all classes get assigned).
