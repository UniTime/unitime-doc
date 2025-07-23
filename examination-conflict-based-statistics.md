---
layout: default
title: Examination Conflict-Based Statistics
---

## Screen Description

The Examination Conflict-Based Statistics screen displays the conflicts created during the solver's attempts to assign possible rooms and periods to the exam (i.e., other examination assignments that were incompatible) and the reasons for these conflicts. These reasons correspond to violations of various constraints on the problem (for example, two examinations requiring a single instructor at the same period, or three examinations requiring the same period when only two rooms are available). Typically, these conflicts are caused by too many examinations competing over a fixed resource. The statistics can help point out the constraining resource, or an overly restrictive requirement, so that changes can be made to the input data which allow the problem to be solved.

![Examination Conflict-Based Statistics](images/examination-conflict-based-statistics-1.png){:class='screenshot'}

## Details

### Filter

* **Mode**
	* Variable - oriented
		* The upper-most level of each problematic set is the variable (examination) whose values (period/room assignments) have been unassigned; the next level are resources and the last one is examinations competing over resources with the given examination
	* Constraint - oriented
		* The upper-most level of each problematic set is the constraint that causes unassignments (such as "Distribution different-day", "Room UNIV 101", etc.)

* **Limit**
	* Percentage of unassignments you want to display (the exams/resources with the largest number of unassignments are displayed first)
	* The limit is applicable to the lower levels too (for example, you will only see examinations covering the most important 50% of the problems with a given resource)

### Examination Conflict-based Statistics

The structure for each mode is as follows

**Constraint-oriented**

* Constraint
	* Examination in the constraint that got unassigned
		* Period, room and instructor for that examination
			* The examination that caused the unassignment of the unassigned examination

**Variable-oriented**

* Examination that got unassigned
	* Period, room, and instructor for that examination
		* Constraint
			* The examination that caused unassignment due to the constraint

## Operations

* **Change**
	* Apply changes in the filter and refresh the displayed data

* **Refresh**
	* Refresh the displayed data

