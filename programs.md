---
layout: default
title: Programs
---

## Screen Description

The Programs screen displays and allows editing of the list of available programs for the current academic session.

![Programs](images/programs-1.png){:class='screenshot'}

Programs are one of the **optional** student curricular properties. Student curriculum may contain the following items:

* [Academic Area](academic-areas) (e.g., college or program of study)
* [Academic Classification](academic-classifications) (e.g., year or semester of study)
* [Major](majors) (e.g., specialization)
* [Concentration](concentrations) (optional, e.g., program/specialization variant)
* [Campus](campuses) (optional)
* [Degree](degrees) (optional, e.g., Master, Bachelor or Certification)
* [Program](programs) (optional)

or

* [Academic Area](academic-areas) (e.g., college or program of study)
* [Academic Classification](academic-classifications) (e.g., year or semester of study)
* [Minor](minors)

A student may contain multiple tuples of (academic area, classification, major, concentration, campus, degree, program) and/or (academic area, classification, minor).

## Properties

Each program contains the following properties:

* External Id
	* External ID of the program
	* External IDs are only editable via the [XML import](xml)
	* Programs with an external ID cannot be deleted. The presence of the External ID indicates that the program has been imported from an external system.

* Abbreviation
	* Program abbreviation

* Title
	* The title of the program

A program may contain one or more majors and/or minors, there are editable on the [Majors](majors) and [Minors](minors) screen.

## Operations

The table can be sorted by any of its columns, just by clicking on the column header and the sorting option that opens.

### Add Program
Click **Add** to add a new program

![Programs](images/programs-2.png){:class='screenshot'}

* Click **Save** to create a new program
* Click **Back** to return to the list without making any changes

### Edit Program
Click a particular program to make changes or to delete the program

![Programs](images/programs-3.png){:class='screenshot'}

* Click **Save** to make changes, **Back** to return to the list without making any changes
* Click **Previous** or **Next** to save the changes and go to the previous or next program respectively
* Click **Delete** to delete a program. Programs with an external ID (i.e., that has been imported from an external system) cannot be deleted.

### Edit Programs
Click **Edit** to edit all Programs

![Programs](images/programs-4.png){:class='screenshot'}

* Use the ![Add](images/icon-add.png) icon to add a new line and ![Delete](images/icon-delete.png) to delete a line
* Programs with an external ID (i.e., that has been imported from an external system) cannot be deleted
* Click **Save** to make changes, **Back** to return to the list without making any changes

### Export CSV/PDF
Click the **Export CSV** or **Export PDF** to export the list of programs to a CSV or PDF document respectively