---
layout: default
title: Additional Distribution Constraints
---
The following additional distribution constraint types can be added into UniTime. They are not present in UniTime out of the box as they have either a special purpose or additional parameters that need to be provided before the distribution constraint can be registered. You can see the registered distribution constraint types on the Administration > Solver > [Distribution Types](distribution-types) page.

To register any of the following constraint types:
1. Download the appropriate XML (also available in GitHub, see [Documentation/Scripts](https://github.com/UniTime/unitime/tree/master/Documentation/Scripts))
2. Use the Administration > Academic Sessions > [Data Exchange](data-exchange) page to import it. This will create a script that will register the appropriate distribution type(s).
3. Use the Administration > Utilities > [Scripts](scripts) page to run the registration script. The script is named Distribution Types: Create XXX Constraints, where XXX is the constraint name.
4. Verify that the distribution types have been registered using the Administration > Solver > Distribution Types page.

### Max Block

Script: [Create Max Block Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Max%20Block%20Constraint.xml)

The MaxBlock constraint checks for too big blocks of back-to-back classes of an instructor on a day.

It has two parameters: a maximal length of a back-to-back block that is allowed and a minimum length of a break between two classes not to be considered in the same block.

Reference `_MaxBlock:120:30_` translates to a maximal block of at most 2 hours (120 minutes) with classes not more than 30 minutes apart.

Implemented by the [MaxBlockFlexibleConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/MaxBlockFlexibleConstraint.java) class.

### Max Break

Script: [Create Max Break Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Max%20Break%20Constraint.xml)

The MaxBreaks constraint limits the number of blocks of non back-to-back classes of an instructor on a day.

It has two parameters: a maximal number of breaks and a minimal length of a break between two classes not to be considered in the same block.

Reference `_MaxBreaks:1:30_` translates to a maximum number of one break (two blocks) on a day of classes not more than 30 minutes apart.

Implemented by the [MaxBreaksFlexibleConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/MaxBreaksFlexibleConstraint.java) class.

### Max Holes

Script: [Create Max Holes Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Max%20Holes%20Constraint.xml)

The MaxHoles constraint limits the number of free time (holes) for an instructor on a day.

It has one parameter: a maximal amount of free time in minutes (between the first and the last class on a day) that an instructor is allowed to have without a penalization.

For example, reference `_MaxHoles:120_` translates to a maximum number of two hours of total free time between the first and the last class on a day.

If required, having more free time is prohibited. If preferred or strongly preferred, the excessive free time is penalized.

Implemented by the [MaxHolesFlexibleConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/MaxHolesFlexibleConstraint.java) class.

### Max Hours A Day

Script: [Create Max Hours A Day Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Max%20Hours%20A%20Day%20Constraints.xml)

The MaxHours constraint limits the number of hours that can be taught on a day.

Classes are to be placed in a way that there is no more than N hours in any day.

Implemented by the [GroupConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/GroupConstraint.java#L713) class (see `ConstraintType.MAX_HRS_DAY`).

### Work Day

Script: [Create Work Day Constraints.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Work%20Day%20Constraints.xml)

The WorkDay constraint limits the number of hours between the start of the first class and the end of the last class on a day.

Classes are to be placed in a way that there are no more than N hours between the start of the first class and the end of the last class on any day.

Implemented by the [GroupConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/GroupConstraint.java#L858) class (see `ConstraintType.WORKDAY`).

### Max Days

Script: [Create Max Days Constraints.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Max%20Days%20Constraints.xml)

Classes must / should be placed in no more than N week days.

The MaxDays constraint limits the number of days of week during which the given set of classes are taught.

It has one parameter: a maximal number of week days during which the given set of classes can be placed.

Reference `_MaxDays:2_` translates to a maximum number of 2 days a week.

Implemented by the [MaxDaysFlexibleConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/MaxDaysFlexibleConstraint.java) class.

### Max Half-Days

Script: [Create Max Half-Days Constraints.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Max%20Half-Days%20Constraints.xml)

Classes must / should be placed in no more than N week half-days. A class starting before noon is considered a morning class, a class starting at noon or later is considered an afternoon class.

The MaxHalfDays constraint limits the number of half-days of week during which the given set of classes are taught.

It has one parameter: a maximal number of week half-days during which the given set of classes can be placed.

A day is split by noon (which can be changed using `General.HalfDaySlot` parameter). A class starting before noon is considered a morning class (despite of its end), a class starting at noon or later is considered an afternoon class.

Reference `_MaxHalfDays:4_` translates to a maximum number of 4 half-days a week.

Implemented by the [MaxHalfDaysFlexibleConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/MaxHalfDaysFlexibleConstraint.java) class.

### Max Weeks

Script: [Create Max Weeks Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Max%20Weeks%20Constraint.xml)

The MaxWeeks constraint limits the number of weeks during which the given set of classes are taught.

It has two parameters: a maximal number of weeks during which the given set of classes can be placed and a day combination indicating what days of the week are considered.If no days of the week are selected, all days of the week are considered.

Reference `_MaxWeeks:3:6_` translates to a maximum number of 3 weeks, but only for classes that are placed on Fridays and Saturdays (64 for Monday, 32 for Tuesday, 16 for Wednesday, 8 for Thursday, 4 for Friday, 2 for Saturday, and 1 for Sunday). If the second parameter is zero, all days of week are considered.

Implemented by the [MaxWeeksFlexibleConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/MaxWeeksFlexibleConstraint.java) class.

### Back-To-Back/Following Weeks

Script: [Create BTB-Following Weeks Constraints.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20BTB-Following%20Weeks%20Constraints.xml)

Back-To-Back Weeks: Given classes must be taught on weeks that are back-to-back (the gap between the two assigned date patterns is less than a week).

When prohibited or (strongly) discouraged: any two classes must have at least a week gap in between.

Following Weeks: Given classes must be taught on weeks that are back-to-back and in the given order.

When prohibited or (strongly) discouraged: given classes must be taught on weeks in the given order with at least one week between any two following classes.

Implemented by the [GroupConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/GroupConstraint.java#L923) class (see `ConstraintType.BTB_WEEKS` and `ConstraintType.FOLLOWING_WEEKS`).

### Max Consecutive Days (new in UniTime 4.6.92 and 4.7.14)

Script: [Create Max Consecutive Days Constraints.xml](https://raw.githubusercontent.com/UniTime/unitime/maint_UniTime46/Documentation/Scripts/Create%20Max%20Consecutive%20Days%20Constraints.xml)

Classes must / should be placed on no more than N consecutive days each week.

Please note that individual weeks are considered when the solver parameter `FlexibleConstraint.CheckWeeks` is set to true (defaults to false).

The MaxConsDays constraint limits the number of consecutive days of the week during which the given set of classes is taught.

It has one parameter: a maximal number of consecutive weekdays during which the given set of classes can be placed.

Reference `_MaxConsDays:2_` translates to a maximum number of 2 consecutive days a week.

Implemented by the [MaxConsecutiveDaysFlexibleConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/MaxConsecutiveDaysFlexibleConstraint.java) class.

### Same Days-Room-Start (new in UniTime 4.6.94 and 4.7.15)

Script: [Create Same Days-Room-Start Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Same%20Days-Room-Start%20Constraint.xml)

Given classes must start at the same time of day, on the same days, and in the same room.

It is the combination of Same Days, Same Start, and Same Room distribution preferences.

When prohibited or (strongly) discouraged: Any pair of classes cannot be taught on the same days during the same time in the same room.

Implemented by the [GroupConstraint](https://github.com/UniTime/cpsolver/blob/master/src/org/cpsolver/coursett/constraint/GroupConstraint.java#L974) class (see `ConstraintType.SAME_DAYS_ROOM_START`).

### Daybreak (new in 4.7.43)

Script: [Create Daybreak Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/master/Documentation/Scripts/Create%20Daybreak%20Constraint.xml)

The Daybreak constraint checks for cases when there is an evening class and a morning class the following day.

There should be at least the given number of hours between an evening class followed by a morning class the next day.

The constraint can also be parameterized by the distance between the two classes: The constraint only triggers when the distance between the two classes is over the provided distance.

### Max (Work) Day Range (new in 4.9.95)

Script: [Create Max Days Range Constraint.xml](https://raw.githubusercontent.com/UniTime/unitime/refs/heads/master/Documentation/Scripts/Create%20Max%20Days%20Range%20Constraint.xml)

Given classes must be taught within the number of consecutive days or work days. This means that between the first and last meeting of all classes in the constraint, there cannot be more than the given number of consecutive days or work days, including the first and last day.

When work days are used: Weekends, holidays, and breaks are ignored. Holidays and breaks are taken from the settings on the [academic session](edit-academic-session). Weekend are the last two days of the week, with the week starting on Monday by default (can be changed using the `General.FirstWorkDay` solver parameter).

The constraint can also be parameterized by the number of consecutive days, and whether only work days or all days are considered.