---
layout: default
title: Instructor Scheduling
---


In UniTime 4.2, a new component for automatic assignment of instructors to classes or courses has been created. The instructors (e.g., teaching assistants) are expected to be assigned after the course timetabling and student scheduling is done, using information from both course timetabling (course timetable) and student scheduling (student availability).

The instructors that are to be automatically assigned to classes are included in the list of instructors (Instructors page), the distinction is made by their maximal load (zero means no automatic assignment) and teaching preferences (prohibited also means no assignment).

The automatic assignment can be based on various instructor attributes that can be defined globally or on a departmental level. These attributes can be grouped by type (e.g., skill or performance level, qualification, certification).

The following data are needed to be entered on instructors (see [Instructor Assignment Preferences](instructor-assignment-preferences) screen):

* List of instructors (e.g., teaching assistants) that can be used for instructor assignment

* Maximal load of an instructor (could be in hours or any other arbitrary units)

* Teaching preference (from strongly preferred to prohibited)

* Attributes of the instructor

* Time requirements and course preferences

* Distribution preference (back-to-back, same days, and same rooms are considered)

The following data are needed to be entered on courses (teaching requests):

* Each teaching request contains a number of instructors needed and the teaching load

* Whether the instructor is to be assigned as course coordinator

* List of classes that the instructor would teach (usually following the parent-child relation)

* List of additional classes during which the instructor must be available (e.g., the lecture)

* Additional information that should be copied over to the instructor assignment (percent share, lead, teaching responsibility)

* Some classes may be allowed to overlap in time, in which case the overlapping time is to be minimized

* Instructor and attribute preferences and requirements

* For instructors that can have multiple assignments, there is a preference for the assignments to be of the **same course** (e.g., a different Lab-Rec pair) and/or to share the **same common** part (e.g., the lecture)

Instructor scheduling considers various hard and soft constraints. The hard constraints include:

* Maximal load of the instructor (each teaching assignment has a load defined, and there is a maximal load defined on each instructor)

* The instructor must be available (unless allowed, there is no other overlapping teaching assignment, the assignment is not during a prohibited time and, if the instructor is also student, he/she does not have any classes at the time of the assignment)

* Instructors with prohibited teaching preference cannot be used

* Required and prohibited attribute, instructor, course preferences must be obeyed

* Required and prohibited same course, same common must be obeyed

* Required and prohibited back-to-back, same day, same room constraints that are set on the instructor must be obeyed

The optimization criteria (soft constraints) include

* If time overlaps are allowed, minimize the total overlapping time

* Maximize the number of satisfied soft preferences (strongly preferred, preferred, discouraged, or strongly discouraged) based on teaching, time, attribute, instructor, course preferences, same course and same common constraints, and back-to-back, same day, same room distribution preferences

* Maximize original assignment in the MPP mode (Minimal Perturbation Problem)

* If a teaching request require two or more instructors, different instructors must be used

* Minimize unused instructor load for instructors with one or more assignments (that is the difference between the maximal load of the instructors and the sum of the loads of the assigned teaching assignments)

The instructor assignments can be computed automatically, using the instructor scheduling solver. After that, manual changes can be made with either the solver still running in memory (and providing suggestions) or without the solver in which case the assignment changes are made directly in the database.

The instructor scheduling problem is solved separately for each department. Only one solution can be saved for each department (like with the examinations). There is a commit process, however, and the actual instructor assignments and course coordinators are only populated when the solution is committed. Otherwise, the teaching assignments that were computed by the solver are only kept on the individual teaching request and they do not show outside of the department.

The instructor attributes can be entered on the [Instructor Attributes](instructor-attributes) page, or on the [Instructor Assignment Preferences](instructor-assignment-preferences) page (accessible from the [Instructor Detail](instructor-detail) page) where additional information like the maximal teaching load and preferences can be entered. Teaching requests are defined on the [Setup Teaching Request](setup-teaching-requests) page (accessible from the [Instructional Offering Detail](instructional-offering-detail) page).

The instructor scheduling solver works much like any other UniTime solver. It can be loaded, unloaded, started, saved, etc. using the Courses > Instructor Scheduling > [Instructor Scheduling Solver](instructor-scheduling-solver) page. There is a [Solver Log](instructor-scheduling-solver-log) page, a page with [assigned](assigned-teaching-requests) and [not-assigned](assigned-teaching-requests) teaching requests, and a page with [changes](teaching-assignment-changes), and a page with [teaching assignments](teaching-assignments). The [Teaching Assignments](teaching-assignments) page provides a view from the instructor perspective whereas the [Assigned Teaching Requests](assigned-teaching-requests) (and [Not-Assigned Teaching Requests](not-assigned-teaching-requests)) show the solutions from the teaching requests / courses perspective. Teaching requests and teaching assignments can be filtered by subject area or department, courses, instructors, or the individual attributes. More details are visible when a line (either a teaching request or a teaching assignment is clicked). The details page allows for manual assignments and can also provide suggestions (when the data are loaded in the solver). It can switch between details of a particular teaching request or a particular instructor.
