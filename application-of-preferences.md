---
layout: default
title: Application Of Preferences
---


**Rule #1: What you see on a class will be used by the solver.**

The (time/room/distribution/...) preferences can be entered in different ways. Below are the rules that are applied when preferences from two different places are combined.

## Instructor Preferences

To use instructors preferences, the user must have inheritance of instructor preferences turned on (in [Manager Settings](manager-settings) - to get there, click on Settings under User Preferences in the left hand side menu)

1. Classes with external manager
	1. Instructor preferences are applied only at the moment when the instructor is being assigned to a class in the [Edit Class](edit-class) screen; if you change that instructor's preferences later, the change won't be reflected on the class
2. Classes with departmental manager
	1. Combination with preferences set only on the scheduling subpart level (not on individual classes): The subpart preferences are combined with instructor's preferences for each class and any changes made to instructor's preferences later are reflected on classes
	2. Combination with preferences set on individual classes (in the [Edit Class](edit-class) screen): The class preferences overwrite instructor's preferences

Recommended usage:

Put preferences on scheduling subparts and on instructors, not on individual classes. Then when an instructor is assigned to a class, the preferences get combined (the stronger wins - so, strongly preferred wins over preferred etc.; negative wins over positive). When an instructor is already assigned and his preferences are changed, so are the combined preferences on his/her classes.

## Subpart Preferences

Subpart preferences are reflected on classes unless overridden on classes

* Examples:
	* The scheduling subpart says "Monday strongly preferred" and the classes did not have any preferences entered - then the classes say "Monday strongly preferred" too
	* The third class of this scheduling subpart needs to be on Tuesday - this preference is set up on this particular class - then the first two classes will still have "Monday strongly preferred" but this preference won't apply to the third class any more

To delete all overrides on classes and keep only the subpart preferences, click on the Clear Class Preferences button in the [Scheduling Subpart Detail](scheduling-subpart-detail) screen

## Class Preferences

Preferences entered in the [Edit Class](edit-class) screen override preferences entered in the [Edit Scheduling Subpart](edit-scheduling-subpart) or [Instructor Preferences](instructor-preferences) screen.

What you see in the [Class Detail](class-detail) screen are the preferences that will be used by the solver during timetabling (these preferences are displayed in many other screens that contain this class, such as [Instructional Offerings](instructional-offerings)). You will either see preferences entered directly on a class or subpart preferences or class/subpart preferences combined with instructor's preferences.
