---
layout: default
title: Examination Solver Status
---


## Description

The Examination Solver Status section is displayed in the lower left hand side corner of the screen (below the menu) when examination solver is being used (otherwise it is a shaded tab next to the [Current User](current-user)).

## Details

* **Owner**
	* The user who started the solver

* **Host**
	* The server on which the solver is running

* **Solver**
	* Information about what the solver is doing
	* Examples:
		* Loading input data...
		* Awaiting commands...
			* This one means that the solver is waiting for your action, such as clicking on the Refresh button and then on Start to start creating a timetable or looking at the timetable or clicking on Unload etc.
		* Solving problem...
		* Solver stopped
		* Saving solution...

* **Phase**
	* The current phase of the solver -- the name of the algorithm it is currently using to solve the problem
	* Examples:
		* Hill climbing
		* Great deluge

* **Progress**
	* Just something to let you know that the solver is not dead

* **Version**
	* Current version of the application

* **Session**
	* Session for which a timetable is being created

You can click on the Examination Solver Status tab any time to refresh it. Otherwise it is refreshed automatically in regular intervals (such as every 10 seconds).
