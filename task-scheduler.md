---
layout: default
title: Task Scheduler
---


## Screen Description

The Task Scheduler page can be used to schedule periodic execution of the existing [Scripts](scripts) within the current academic session.

![Task Scheduler](images/task-scheduler-1.png){:class='screenshot'}

## Details

Each task has the following properties

* **Name**
	* Task name

* **Owner**
	* Administrative user who created the task

* **Script**
	* Script to be periodically executed

* **Parameters**
	* Script parameters (depending on the script)

* **Dates**
	* Dates when the script is to be executed

* **Time**
	* Start time

* **Status**
	* **Created** ... a task execution has been created and is scheduled to be executed
	* **Queued** ... a task execution is queued for the execution (only one script can be running at a time)
	* **Running** ... a task execution is being executed
	* **Finished** ... a task execution has finished
	* **Failed** ... a task execution has failed

It is possible to roll scheduled tasks from one academic session to the next using the [Roll Forward Session](roll-forward-session) page. The dates are relative to the academic session start date.

## Operations

The table can be sorted by any of its columns, just by clicking on the column header and the sorting option that opens.

### Task Details

More details can be seen when clicking on a task, including the log and output files for the executions that have already finished. This will show the [Task Details](task-details) page.

### Add Task
Click the **Add New** button to create a new task

![Task Scheduler](images/task-scheduler-2.png){:class='screenshot'}

* Click **Save** to create a new task
* Click **Back** to close the Add Task dialog without making any changes

### Refresh

Click the **Refresh** button to refresh the page

