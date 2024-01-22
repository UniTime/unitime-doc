---
layout: default
title: Solution Properties
---


## Properties of a saved timetable

* **Created**
	* Date and time when the timetable was saved

* **Settings**
	* The solver configuration with which the timetable was created (for example, Default, or Interactive - see the Notes section in the description of the [Solver Configurations](solver-configurations) screen)

* **Committed**
	* If this timetable has been committed, the date and time of that event is displayed

* **Owner**
	* The solver group who saved this timetable (usually the department whose deputy saved the timetable)

* **Assigned variables** (Assign)
	* The percentage of classes that got time and room (out of all loaded classes); if it is not 100%, the timetable is incomplete

* **Overall solution value** (Total)
	* Value of the optimization function for this timetable; the value is based on criteria used to generate the timetable; the lower the better
	* Note: You should not compare this value for two different timetables, even if created for the same set of data - the value is comparable only between different stages of solving one timetable

* **Time preferences** (Time)
	* Percentage of time preferences met

* **Student conflicts** (Stud)
	* Number of [student conflicts](student-conflicts) (committed, distance, hard)

* **Room preferences** (Room)
	* Percentage of room preferences met

* **Distribution preferences** (Distr)
	* Percentage of distribution preferences met

* **Back-to-back instructor preferences** (Instr)
	* Percentage of back to back classes taught by the same instructor which are in rooms close enough for the instructor to walk from one to the other

* **Too big rooms** (TooBig)
	* "Too big room" is a room that has at least 25% more seats than is necessary for the class that has been timetabled there. There are two limits for Too big rooms - 25% and 50% more seats than necessary. Rooms exceeding the number of necessary seats by less than 25% are not penalized (penalty "0"), rooms exceeding the necessary seats by 25% to 50% are penalized by "1", rooms with more than 50% more seats than necessary have penalty "4". The number in parenthesis is the total penalty over all classes. The percentage can be interpreted as "0% - all classes are in rooms that do not have more than 125% of necessary seats, 100% - all classes are in rooms that have more than 150% of necessary seats".

* **Useless half-hours** (Useless)
	* Percentage of unused time slots (five minutes intervals) in all rooms that are hard to use for regular classes for one of the following reasons (each reason is represented by a number next to the percentage)
		* The time slot is in a block between classes that is half an hour or shorter (with a class on either side)
		* The time slot is in a part of a broken time pattern, i.e., it is on Tuesday at 9:05 while on Thursday 9-10:30am there is already a class - so a standard time pattern TR 9am-10:30am cannot be used

* **Perturbations: Total penalty** (Pert)
	* Only in the MPP configuration
	* Penalty for changes made to a timetable after it was loaded from a saved solution

* **Note**
	* A note about the timetable
	* Editable once the timetable is selected (to select a timetable, click on its line in Saved Timetables)

## Properties of a selected solution

* **Created**
	* Time and date when the solution was created (saved)

* **Owner**
	* Solver group which owns the solution

* **Commited**
	* Information whether a solution is committed (it is either Not committed or it contains time and date when it was committed)

* **Note**
	* Solution note


 See properties of a loaded solution for the remaining properties

## Properties of a loaded (current/best) solution

* **Created**
	* Time and date when the solution was created

* **Assigned variables**
	* Percentage of classes that have time and room assigned (the number of assigned classes / total number of classes is in brackets).

* **Overall solution value**
	* Value of the objective function that is used by the solver to evaluate a solution. When comparing two solution (of the same solver group and loaded using the same solver configuration), the value with lower value is better. See [Solver Configurations](solver-configurations) for details.

* **Time preferences**
	* Overall satisfaction of time preferences expressed as percentage (100% all classes assigned in the best possible times, 0% all classes assigned in the worst possible times). The number next to the percentage is the sum of normalized time preferences of all assigned classes.

* **Student conflicts**
	* Number of [student conflicts](student-conflicts) (committed, distance, hard)

* **Room preferences**
	* Overall satisfaction of room preferences expressed as percentage (100% all classes assigned in the best possible rooms, 0% all classes assigned in the worst possible rooms). The number next to the percentage is the sum of normalized room preferences of all assigned classes.

* **Distribution preferences**
	* Overall satisfaction of distribution preferences expressed as percentage (100% all distribution preferences met, 0% no distribution preference met). The number next to the percentage is the sum of normalized distribution preferences.

* **Back-to-back instructor preferences**
	* Percentage of back to back classes taught by the same instructor which are in rooms close enough for the instructor to walk from one to the other. The number next to the percentage is the weighted number of back to back classes of the same instructor (the weights depend on the distance between the rooms)

* **Too big rooms**

* "Too big room" is a room that has at least 25% more seats than is necessary for the class that has been timetabled there. There are two limits for Too big rooms - 25% and 50% more seats than necessary. Rooms exceeding the number of necessary seats by less than 25% are not penalized (penalty "0"), rooms exceeding the necessary seats by 25% to 50% are penalized by "1", rooms with more than 50% more seats than necessary have penalty "4". The number in parenthesis is the total penalty over all classes. The percentage can be interpreted as "0% - all classes are in rooms that do not have more than 125% of necessary seats, 100% - all classes are in rooms that have more than 150% of necessary seats".

* **Useless half-hours**
	* Percentage of unused time slots (five minutes intervals) in all rooms that are hard to use for regular classes for one of the following reasons (each reason is represented by a number next to the percentage)

	1. The time slot is in a block between classes that is half an hour or shorter (with a class on either side)
	2. The time slot is in a part of a broken time pattern, i.e., it is on Tuesday at 9:05 while on Thursday 9-10:30am there is already a class - so a standard time pattern TR 9am-10:30am cannot be used

* **Same subpart balancing penalty**
	* Penalty if the classes of a subpart are not distributed evenly over different parts of a day
	* Calculated from number of hours that are used more than would be an average over available times

* **Department balancing penalty**
	* Penalty if classes of a department are not distributed evenly over different parts of a day (to be fair to departments and not give one department all the 10am - 2pm slots)

* **Perturbation variables**
	* Only in MPP solver mode
	* The number of classes that have a time or room assignment different from the one in the loaded timetable + the number of new variables that were not in the loaded timetable

* **Perturbations: Total penalty**
	* Only in MPP solver mode
	* Penalty for changes made to a timetable after it was loaded from a saved solution

* **Time**
	* The time it took the solver to create this timetable

* **Iteration**
	* Number of iterations performed to create this timetable

* **Memory usage**

* Memory allocated on the solver server where the instance is loaded

* **Speed**

* Number of iterations per second
