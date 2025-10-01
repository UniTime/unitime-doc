---
layout: default
title: Examination Timetabling
---

UniTime builds a complete exam schedule each term that minimizes the number of conflicting exam placements for all students. It can also minimize the number of occurrences of back-to-back exams or students with more than a given number of exams in a day. This is particularly useful for colleges and universities that frequently update class offerings or have a large number of multi-section courses that do not fit well into mapped exam timetables.

UniTime can be used to create schedules for mid-term exams as well as for final exams.

Please see the [system demonstration](https://demo.unitime.org) or [contact us](mailto:support@unitime.org) for more information.

Additional resources:
* [Examination Timetabling Manual](manuals/examination-timetabling)
* [UniTime System Highlights](https://www.unitime.org/unitime_intro.php) [[pdf](https://www.unitime.org/present/unitime-highlights.pdf)]
* [Real-life Examination Timetabling](https://www.unitime.org/papers/mista13.pdf)
* [Benchmark Data Sets](https://www.unitime.org/exam_datasets.php)

## Examination Problem

Examination timetabling problem consists of the following entities

* A set of non overlapping **examination periods**. Each examination period has defined a date, a start time and a length. It may also have a preference associated with it. The preferences that are set on periods act as default preferences for all examinations (e.g., we can discourage the last day of the examination week if desired).
	* So for instance, five 2 hour long periods can be defined for each day of the examination week for final exams, or an early and a late period can be defined for each date during the semester on which midterm examinations can take place.

* A set of **rooms**. Each room has a normal and an examination seating capacity defined. Additionally, a room has a room availability matrix defined (stating during which periods a room can be used) and each period can be associated with a preference as well. Room coordinates may be provided as well. The following preferences can be set on a room for each period
	* Prohibited ... a room cannot be used during this period
	* Strongly Discouraged ... a room can only be used for an exam, the exam has a preference for this room (an exam overrides the preference of the room).
	* Discouraged ... a use of the room during this period should be minimized (Note that an exam is put into such a room if there is no other room of enough size available. This means that an exam will not be split into multiple rooms if it can be placed in a discouraged room.)

* A set of **examinations**. Each exam has defined a length, type of seating, maximal number of rooms into which it can be split (typically between 1 to 4), and a list of students enrolled in the exam (e.g., by providing the list of courses, or classes for which the exam is organized). If the maximal number of rooms is set to zero, an exam is not to be placed in a room, it is only assigned to a period. One or more instructors may be associated with an exam. Additionally, each exam can have the following requirements and preferences associated with it:
	* **Period preferences**: a preference or requirement for each period. These may include prohibited periods (an exam cannot be placed in such period) or required periods (an exam must be placed in the period)
	* **Room preferences**: a preference or requirement on rooms, buildings, room features and/or room groups. These may include prohibited or required rooms, buildings etc.

* A set of **distribution preferences**. A distribution preference is set between two or more exams, it can be either required or with a preference. Distribution preferences are of the following types:
	* Same Room ... exams are required/preferred to take place in the same room or rooms.
	* Different Room ... exams are required/preferred to take place in different rooms (no two exams of the constraint are to be placed in the same room).
	* Same Period ... exams are required/preferred to take place during the same periods.
	* Different Period ... exams are required/preferred to take place during different period.
	* Precedence ... exams are required/preferred to take place in the order they are listed in the constraint. For instance if exam A is in the precedence constraint before exam B, it is to be placed in a period that precedes the period in which exam B is placed.

## Hard Constraints

Examination timetabling problem is a problem of assigning exams to examination periods and rooms so that the following constraints are respected.

* Only one exam can be placed in a room at any period.

* A room cannot be used on periods during which it is not available or marked as prohibited. A room can only be used during a period marked as strongly discouraged by an exam that has a preference for this particular room.

* An exam must be placed in a room (or a set of rooms) so that the overall seating capacity of the rooms equals or is greater than the number of students attending the exam, with respect to the requested seating type (e.g., each room has a normal seating and examination seating capacities defined, an exam can request either normal or examination seating). Maximal number of rooms into which an exam can be split cannot be exceeded as well.

* An exam cannot be placed in a period that is marked as prohibited for the exam, or that is not required if there is some other period required by the exam. Similarly, an exam cannot be placed in a room that is prohibited for the exam (by the room requirements that are set on the exam).

* Required distribution constraints must be satisfied.

## Soft Constraints (Optimization Criteria)

During the search, besides looking for a complete solution (all exams are assigned to periods and rooms) that satisfies all hard constraints mentioned above, the following criteria are optimized. Each criterion has a weight associated with it (e.g., direct conflicts have typically much higher weight that back-to-back conflicts), overall weighted sum of the above criteria is minimized.

### Student Conflicts

* Direct Conflicts: A student is enrolled in two exams that are placed in the same period.

* More Than Two Exams A Day Conflicts: A student is enrolled into three or more exams that take place on the same day.

* Back-To-Back Conflicts: A student is enrolled into exams that are scheduled in consecutive periods (back-to-backs over an end of a day may or may not be considered).

* Distance Back-To-Back Conflicts: A student is enrolled into exams that are scheduled in consecutive periods and placed in rooms that are too far apart (if multiple rooms are involved, the maximal distance is considered, by default a threshold of 670 meters is used).

### Instructor Conflicts

* Direct Conflicts: An instructor is associated with two exams that are placed in the same period.

* More Than Two Exams A Day Conflicts: An instructor is associated with three or more exams that take place on the same day.

* Back-To-Back Conflicts: An instructor is associated with exams that are scheduled in consecutive periods (back-to-backs over an end of a day may or may not be considered).

* Distance Back-To-Back Conflicts: An instructor is associated with exams that are scheduled in consecutive periods and placed in rooms that are too far apart

### Other Criteria

* Period Penalty: A penalization of an assignment of an exam into a period that is not preferred by the exam. Penalization corresponds to the preference that is put on the period for the exam. It is basically a difference of the best possible period and the assigned one, e.g., if there is a preferred period (weight -1), but the exam is assigned to discouraged period (weight 1), the period penalty for the exam is 2. Overall, preferences are wighted as follows:
	* Strongly Discouraged .. 4
	* Discouraged .. 1
	* Neutral .. 0
	* Preferred .. -1
	* Strongly Preferred .. -4

* Room Penalty: A penalization of an assignment of an exam into a room that is not preferred by the exam. Penalization corresponds to the preference that is put on the room for the exam (e.g., if there is a preference on a building on the exam, the preference is applied to all rooms of the building), same weighting scale as for period penalty is used.

* Distribution Penalty: A penalization of each distribution preference (that is not required) that is not satisfied is considered. Penalization corresponds to the preference that is associated with the constraint (1 for preferred, 4 for strongly preferred).

* Room Split: A penalization of assigning an exam into multiple rooms. There is penalty of 1 of splitting an exam into two rooms, 4 into three rooms, 9 into four rooms (it is (r-1)^2 where r is the number of rooms into which an exam is assigned).

* Room Split Distance: Average distance between rooms that an exam is split.

* Room Size: A penalization of using rooms that are two large for an exam. It is the difference of the size of the room (either exam or normal seating based on what is required by the exam), and the size of the exam (number of students enrolled in the exam).

* Rotation Penalty: An exam can have an average period (computed from the previous examination problems) associated with it. If so, a penalty of the current period index multiplied by the average period index is associated with each exam. This effectively "rotates" the exams (exams that were later in the examination term has higher penalty if placed in a later period).

* Large Exams Penalty: One for each large exam (an exam with more than a certain number of students enrolled) if it is placed on or after a certain period

### Minimal Perturbation Problem

* Perturbation Penalty: If initial exam assignments are provided, a penalization of putting an exam into a different period based on the distance of the two periods and the size of the exam can be included in the optimization criteria.
