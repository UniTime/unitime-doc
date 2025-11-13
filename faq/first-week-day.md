---
layout: faq
title: First Day of a Week
---
## Question

Our week starts on Sunday, how we can change UniTime to display time patterns and others starting on Sunday?

## Answer

There are a few configuration parameters (that can be set on the Administration > Defaults > [Configuration](../application-configuration) page, or in the custom properties) that change the display so that a week starts on Sunday.

- [Time Patterns](../time-patterns): First day of week (0 is Monday, 1 is Tuesday, etc.)
    - `unitime.timePattern.firstDayOfWeek=6`
- [Events Time Grid](../events): First day of the week (0 is Monday, 1 is Tuesday, etc.)
    - `unitime.events.gridStartDay=6`
- [Timetable Grid](../timetable): First day of week (0 is Monday, 1 is Tuesday, etc.)
    - `unitime.timeGrid.startDay=6`
- [Timetable Grid](../timetable): Create an additional option in the **Days** drop-down from Sunday to Thursday
    - `unitime.timeGrid.days14=1111001\|Sunday - Thursday`
    - There is one property for each available option starting with 1, the format is bitmap\|name

And in the solver configuration, the following two parameters need to be created in the General Settings section on the Administration > Solver > [Parameters](../solver-parameters) page and set as follows:

1) First Day of a Week
```
Name: General.FirstWorkDay
Description: First Day of Week (0..Monday, 1..Tuesday,...)
Type: integer
Default: 6
```

2) Last Work Day of a Week
```
Name: General.LastWorkDay
Description: Last Work Day of Week (0..Monday, 1..Tuesday,...)
Type: integer
Default: 4
```