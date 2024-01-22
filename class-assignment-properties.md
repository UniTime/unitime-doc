---
layout: default
title: Class Assignment Properties
---



 Each class assignment has properties displayed in various screens (for example, in [Assigned Classes](assigned-classes)). All the displayed properties are described here, not only the properties displayed in the simplified mode.

* **Class**
	* Subject area, course number, instructional type and class number within that type (for example, ECET 107 Lab 1)

* **Date**
	* Date pattern for a given class (for example, Full Term)

* **Time**
	* Assigned time

* **Room**
	* Assigned room(s)

* **Instructor**
	*   An instructor(s) for the class for whom conflict checking is performed
		* Note: If there is an instructor assigned to a class for whom conflict checking is not required, the person will not be displayed here (the person is not taken into account during timetabling at all)

* **Students** or **Std**
	* Change in the number of [student conflicts](student-conflicts) caused by this assignment


 The additional properties in case when the simplified mode is not used are

* **Time** (Tm)
	* Change in penalty for unmet time preferences caused by this assignment
		* This is a difference between the best possible time assignment and the currently assigned time

* **Room** (Rm)
	* Change in penalty for unmet room preferences caused by this assignment
		* This is a difference between the best possible room assignment and the currently assigned room(s)

* **Distribution Preferences** (Gr - Group Constraints)
	* Change in penalty for unmet distribution preferences
		* Weight of the distribution preferences that the class is involved in that are not satisfied

* **Back-to-back instructor preferences** (Ins)
	* Change in penalty for unmet back-to-back instructor preferences caused by this assignment
		* It is discouraged for an instructor to teach two classes that are back-to-back and placed in different buildings (distance>0)
		* It is strongly discouraged for an instructor to teach two classes that are back-to-back and placed in rooms that are more than 50 meters apart
		* It is prohibited to assign two classes that are taught by the same instructor back-to-back to rooms that are more than 250 meters apart
			* The last criterion can be ignored for a particular instructor, see [Edit Instructor](edit-instructor) page, Ignore Too Far toggle
			* These instructor back-to-back distance constants can be changed in the solver configuration, see [Solver Configurations](solver-configurations) page

* **Useless half-hours** (Usl)
	* Change in the effectiveness of using time
		* There is a strongly discouraged penalty for leaving unoccupied time windows that are 30 minute long (or less) in the rooms
		* There is a discouraged penalty for using times that are breaking standard Tuesday-Thursday and Monday-Wednesday-Friday time patterns (e.g., if the Monday and Wednesday time is occupied, but Friday is left unoccupied)

* **Too big rooms** (Big)
	* Change in penalty for using rooms which are too large
		* It is discouraged to use a room that is 25% larger than the smallest available room
		* It is strongly discouraged to use a room that is 50% larger than the smallest available room

* **Departmental Balancing** (Dept)
	* Change in penalty for departmental balancing (= fairness of class distribution over times - for example, one department should not have all classes around noon and another department at 7am, they should share)

* **Same subpart balancing** (Subp)
	* Change in penalty for classes of the same subpart
		* Note: there is a penalty if classes are not distributed evenly - for example, if there are seven possible times for ten classes of the same scheduling subpart, there should be at most two such classes at a time

* **Perturbation penalty** (Pert)
	* Change in perturbation penalty caused by this assignment
		* This is only applicable when the solver is loaded in MPP (minimal perturbation problem) mode
		* Various weights can be assigned to different changes between the original and the new solution using [Solver Configurations](solver-configurations) page


 Note: for all of these properties, negative values mean improvements, positive values mean penalty for the timetable caused by this assignment.
