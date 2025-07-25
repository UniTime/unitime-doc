---
layout: default
title: Alternatives for Class
---


## Screen Description

The Alternatives screen offers alternatives for classes in the [Student Scheduling Assistant](student-scheduling-assistant) screen. Some alternatives may include changes in the times/rooms of other classes, but in that case, all changes are described as part of the alternatives.

![Alternatives for Class](images/alternatives-for-class-1.png){:class='screenshot'}

## Details

There is color coding for the proposed changes:

* <span style='color:blue;'>Blue</span>: the class on which the user clicked will be moved in time or room
* Black: another class will be changed, but it will still be a part of the student's timetable
* <span style='color:red;'>Red</span>: a class will be removed from the student's timetable to make space for the suggested alternative; this way, it is also possible to assign a course with lower priority at the cost of removing a course with higher priority

### Filter

Filter assignments of the selected class by name, day, start time, date, room, or instructor. Hit **Search** to update the list of alternatives.

You can also use the following tags:
* *name:* class name
* *day:* class must meet on this day or days (e.g., monday, MWF
* *time:* class must start at this time (e.g., 730)
* *before:* class must end before or by this time
* *after:* class must start on or after this time
* *date:* class must meet on this date
* *room:* class must use this room or building
* *instructor:* class must have this instructor
* Use *or*, *and*, *not*, and brackets to build a boolean query.
* Example for a Monday class starting at 7:30 am or 8:30 am:
 ```
 day: monday and (time: 730 or time: 830)
 ```

### Operations

Click on the alternative that should be part of the timetable to apply the changes and return to the [Student Scheduling Assistant](student-scheduling-assistant) screen. To leave the screen without applying any changes, click outside the Alternatives window. Hovering over an alternative will show what the new schedule would look like in a grid.

Click **Drop** to remove the course from the schedule.


When the course can be wait-listed, click **Wait-List** to wait-list the course. This is useful when the course is full (there are no alternatives available), or when you would like to wait-list for a particular section that is currently full.

