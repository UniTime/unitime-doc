---
layout: default
title: Student Scheduling Solver
---


## Screen Description

In the Student Scheduling Solver screen, the user can run the sectioning solver to assign classes to students whose course requests have been entered into the system. The assignment is based on the timetable, the student requests and, if needed, on the last-like or curriculum course demands (in case only a part of current student course requests are available).

## Solver not started

### Solver

* **Status**
	* Current status of the solver

* **Solver configuration**
	* Configuration - see [Solver Configurations](solver-configurations) for more information
	* Chose the appropriate configuration from choices listed

* **Solver mode**
	* Options
		* Initial - starts scheduling students with no previous assignments
		* MPP - continues working on the loaded schedule, trying to find a better schedule for the students with as few differences from the loaded one as possible
		* Projection - the real student enrollments are complemented with projected student course demands (the options for which demands are in the "Projected student course demands" drop down list);

* **When finished**
	* Choose what to do when the time-out limit on the solver is reached

* **Student weights**
	* Options
		* Priority - priorities entered by students in their course requests are considered
		* Equal - no priorities considered, all requests have equal weight
		* Legacy - deprecated (used in previous versions of UniTime)
	* See Notes at the end of this page for more details about the options Priority and Equal

* **Projected student course demands**
	* Select, what type of student course requests should be used when not all real student enrollments are available
	* Options
		* None
		* Last Like Student Course Demands
		* Projected Student Course Demands
		* Curricula Course Demands
		* Curricula Last Like Course Demands
		* Student Course Requests
	* Enrolled Student Course Demands

* **Host** (admin)
	* Select server you want to run the solver on (setting "auto" means that the least occupied solver will be used; this is the default behavior for non-administrator users)

### Operations

* **Load**
	* Load all input data necessary for student sectioning

* **Start**
	* Load all necessary data and start student sectioning

* **Refresh**
	* Refresh this screen

## Loading input data

During the loading phase, input data are loaded.

### Solver

* **Input data loaded**
	* Time stamp from the time when the latest load of input data started

For the rest, see above.

### Current Student Schedule

The Current Student Schedule is empty during the loading phase.

### Operations

* **Refresh**
	* Refresh this screen
		* When loading is done, new buttons will appear

## Awaiting commands

### Current Student Schedule

The Current Student Schedule has been loaded into the solver together with the input data. The section for the Current Student Schedule has one operation: Store To Best - store the current student schedule to the Best Student Schedule Found So Far.

### Operations

* **Start**
	* Start the solver which will section students

* **Reload Input Data**
	* Reload input data while keeping the current student schedule
		* The assignments that are no longer valid due to the change in the input data will be unassigned

* **Save**
	* Save the Best Student Schedule Found So Far

* **Clear**
	* Clear the student-class assignments

* **Unload**
	* Unload all data and the student schedule from the solver

* **Refresh**
	* Refresh this screen

## Solving problem

### Solver

See above

### Operations

* **Stop**
	* Stop the solver

* **Refresh**
	* Refresh this screen

## Solver stopped

### Best Student Schedule Found So Far

During the automated scheduling (when the solver is running), the best student schedule found so far is saved here. It is the schedule that is presented to the user when they stop the solver or when the time-out is reached.

When the user interacts and makes changes, they can save intermediate results as "Best Student Schedule Found So Far" and later come back to this schedule if the current one is not good.

### Current Student Schedule

When solver is stopped, the Best Student Schedule Found So Far is the same as the Current Student Schedule. If the solver is running, you can see the current solution it is working with in this section.

Operations

* **Restore From Best**
	* Discard the current student schedule and start again from the best student schedule found so far

* **Store To Best**
	* Overwrite the Best Student Schedule Found So Far with this current student schedule

### Problems

The list of warnings appears if any problem occurred during the data load. If there is a problem during solving, there will be an error message (such as Error: FATAL).

### Operations

* **Start**
	* Restart the solver from the current student schedule

* **Reload Input Data**
	* Reload the data from the Input Data section without loosing the assignments in the current student schedule; only prohibited assignments will be lost if breaking hard constraints is not allowed

* **Save**
	* Save the best student schedule found so far
	* Student class enrollments are saved for real students; projected demands are used to update class expected demands for online student scheduling

* **Clear**
	* Clear student-class assignments

* **Unload**
	* Unload both the input data and the student schedule from memory (any student schedule will be lost unless saved in the Best Student Schedule Found So Far section)

* **Refresh**
	* Refresh this screen

## Notes

Description of the student weights as written in UniTime 3.3 Release Notes

P**riority student weighting model**

* First priority request has better weight than all the rest

* Total weight for a student should be between zero and one, one for a fully satisfied student

* Request weight: 1st priority 0.501, 2nd priority 0.250, 3rd priority 0.1248, 4th priority 0.0623, ... (1/2 for alternatives, e.g., 0.2505 for the first alternative of a course)

* 1/2 and 1/4 for the alternatives; but the difference will be distributed down-wards (student has more weight to get the n+1, n+2, ... priority courses)

* Weights are rounded to four digits

* The rest to 1 -- put to the last request or split evenly between all of them.

**Alternative (equal) weighting model**

* All course (non alternative) requests have equal weight (priority is ignored)

* First alternatives have lower weight than first choices, but equal among themselves

* Second alternatives have lower weight than first alternatives, alternative course requests than second alternatives

**There are three ways to use student sectioning**

* When all students are preregistered, the projected demand is none

* If only some students are preregistered, loading and solving preregistered and projected demands together allows students use of online scheduling

* Projection mode is used to recalcule the projected demands
