---
layout: default
title: Solver Warnings
---

This page contains a list of infos/warnings/errors that can be obtained during data load.

| **Type** | **Message** | **Note** |
| :--: | :----------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------- |
| **INFO** | No student enrollments for offering O. | There are no last-like semester student enrollments for instructional offering O. Classes of this offering might require a special attention, since they will not create any student conflicts with other classes. |
|**WARN**| Class C has no available room(s) (class not loaded). | There are no available rooms for class C. This can, for instance, mean that there are no rooms that are not prohibited by the class preferences and that are of sufficient size. |
|**WARN**| Class C has no time pattern selected (class not loaded). | Class C does not have a time pattern selected, but it has a non-zero number of minutes per week. |
|**WARN**| Class C has no available time (class not loaded). | There are no available times for class C. This can, for instance, mean that all the times of the selected time pattern(s) are prohibited by the class preferences. |
|**WARN**| Class C has no available placement (class not loaded). | Class has available time(s) and room(s) but there is no valid combination (e.g., because of room sharing and/or instructor or room availability).Such a class is only loaded in the interactive mode of the solver. |
|**WARN**| Class C has no available placement (after enforcing consistency between the problem and committed solutions, class not loaded). | A reason for inconsistency (conflicting constraints &amp; assignments) is provided as the following INFO message – check the solver log in this case. Such a class is only loaded in the interactive mode of the solver. |
|**WARN**| Unable to assign C &lt;- Time Room (placement not valid) | Assignment from the loaded solution is no longer valid (given time/room became prohibited for some reason). |
|**WARN**| Unable to assign C &lt;- Time Room : reason | Assignment from the loaded solution is no longer valid (because of some other assignment or a new constraint) |
|**WARN**| Class C has zero class limit. | Class has zero class limit. Such a class might require special attention since no students will be sectioned in it and therefore it will not create any student conflicts with other classes. |
|**WARN**| Same instructor and overlapping time required: C1 &lt;- time1 room1, C2 &lt;- time2 room2 | Classes C1 and C2 are requiring same instructor and a single time each, but these times are overlapping (an instructor cannot teach two classes at the same time). |
|**WARN**| Same room and overlapping time required: C1 &lt;- time1 room1, C2 &lt;- time2 room2 | Classes C1 and C2 are requiring a single time and a same room, but these times are overlapping (a room cannot accommodate two classes at the same time, unless there is a Can Share Room distribution constraint between these classes) |
|**WARN**| Class C requires an invalid placement time room : reason | Class C requires a single time and a single room, but the given time/room is not valid because of some other (committed) assignment. |
|**WARN**| Lecture C not found/loaded, but used in distribution preference P | Class C is used by a distribution preference P, but it was not loaded because of some other reason or because it is of different problem (that does not yet contain a committed solution). |
|**WARN**| Distribution preference P refers to less than two classes. | Distribution preference P contains only one class – it is required that each distribution constraint is defined between two or more classes. |
|**WARN**| Inconsistent course reservations for course C. | Course reservations of course offering C are inconsistently set on classes of the course offering C. |
|**WARN**| Cross-listed course C does not have any course reservation. | Cross-listed course offering C does not have any course reservation defined. |
|**WARN**| Total number of course reservations is bellow the offering limit for instructional offering O (total&lt;limit). | Total number of course reservations for the instructional offering O is not equal to the appropriate instructional offering limit. It is below that limit. |
|**WARN**| Total number of course reservations exceeds the offering limit for instructional offering O (total&gt;limit). | Total number of course reservations for the instructional offering O is not equal to the appropriate instructional offering limit. It is above that limit. |
|**WARN**| No reserved space for students of offering C. | Course reservation of course offering C is zero, but there are some last-like student enrollments for this offering in the database. |
|**WARN**| Class limit exceed for class C (nrStudents&gt;classLimit) | Section algorithm enrolled more students into the class C than it is allowed by the class limit. Possible reasons: inconsistent course reservations set on classes (e.g., reservation is for 50 students, but only one section of 25 is reserved), total number of course reservations is not equal to offering limit, configuration limit is smaller than total class limit of a scheduling subpart, or classes of mixed ownership in a subpart (warning can be ignored in this case) |
|**WARN**| Student S enrolled to invalid class C. | This can happen in the case of inconsistent course reservations (set on class level) -- there is no class the given student can be enrolled to. |
|**WARN**| Unable to load input data, reason: exception | Do not continue, do not unload the solver, please contact your UniTime support using the Contact Us  page. |

**Hint:** If you see a **FATAL** message, keep the solver in the memory and use [Contact Us](contact-us) page (located in Help menu) to report a problem.
