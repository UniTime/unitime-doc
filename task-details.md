---
layout: default
title: Task Details
---


## Screen Description

The Task Details page can be used to show (and edit) details of a particular scheduled task. It also allows to show individual runs, their output files, and execution logs.

![Task Details](images/task-details-1.png){:class='screenshot'}

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

Individual executions are shown in the **Scheduled Executions** table. Besides of the date and time of the execution, the line contains the queued, started, and finished time stamps, execution status and the last status message, and the resultant file (when available).

## Operations

Click the execution line to see the log.

Click the Output file to download the resultant file (only visible when at least one execution has produced a file)

### Edit Task

Click **Edit Task** to modify the task. This will open the Edit &lt;Task Name&gt; dialog.

![Task Details](images/task-details-2.png){:class='screenshot'}

* Click **Update** to update the task task
* Click **Back** to close the dialog without making any changes

**Note:** Past executions of the task will not be deleted when a task is updated.

### Delete Task

Click **Delete Task** to delete this task and go back to the [Task Scheduler](task-scheduler) page.

### Back

Click **Back** to go back to the [Task Scheduler](task-scheduler) page.
