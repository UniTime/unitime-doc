---
layout: default
title: Solver Configurations
---


## Screen Description

The Solver Configurations screen provides a list of solver configurations that can currently be used. See the Notes section below for some examples.

## Details

* **Reference**
	* Unique name of the configuration

* **Name**
	* Name of the configuration which is displayed in the screens where the configuration is used

* **Appearance**
	* Names of screens in which this configuration appears (can be used)

Click on any solver configuration to go to its [Edit Solver Configuration](edit-solver-configuration) screen. This screen will also provide you with a lot more information about a given configuration than what can be seen in the list.


![Solver Configurations](images/solver-configurations-1.png){:class='screenshot'}

## Operations

* **Add Solver Configuration** (Alt+A)
	* Add a new solver configuration in the [Add Solver Configuration](add-solver-configuration) screen

## Notes

As an example, here is a brief description of three configurations present in the [online demo](https://www.unitime.org/uct_demo.php) for course timetabling:

* **Check**
	* Purpose: Check if input data is consistent and whether there is a complete (feasible) timetable consistent with the input data
	* The solver does not optimize the solution
		* Solution Comparator Weights are all set to 0
		* Placement Selection has most optimization parameters set to 0
		* The solver stops when a complete solution is found

* **Default**
	* Purpose: Create an optimized timetable consistent with the input data
		* Most parameters have their default values

* **Interactive**
	* Purpose: Create a timetable manually and/or make changes to an existing timetable that do not need to be consistent with the input data
		* It is allowed to break hard constraints (such as required/prohibited times/rooms)
		* The distribution preference "Different Time" is used for classes of the same instructional offering (such as lecture & lab that go together) instead of "Same Students" - this makes it possible to e.g. place a lecture to a place far away from the lab, which would not be possible with the "Same Students" constraint
