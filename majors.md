---
layout: default
title: Majors
---


## Screen Description

The Majors screen displays and allows editing of the list of available majors for the current academic session.

![Majors](images/majors-1.png){:class='screenshot'}

Majors are one of the student curricular properties, typically used to express a specialization. Each major belongs to a particular academic area. Student curriculum may contain the following items:

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

Each major contains the following properties:

* External Id
	* External ID of the major
	* External IDs are only editable via the [XML import](xml)
	* Majors with an external ID cannot be deleted. The presence of the External ID indicates that the major has been imported from an external system.

* Code
	* Abbreviation/Code of the major

* Name
	* Name of the major

* Academic Area
	* Academic area to which the major belongs

A major may contain one or more concentrations (variants), there are editable on the [Concentrations](concentrations) screen.

## Operations

The table can be sorted by any of its columns, just by clicking on the column header and the sorting option that opens.

### Add Major
Click **Add** to add a new major

![Majors](images/majors-2.png){:class='screenshot'}

* Click **Save** to create a new major
* Click **Back** to return to the list without making any changes

### Edit Major
Click a particular major to make changes or to delete the major

![Majors](images/majors-3.png){:class='screenshot'}

* Click **Save** to make changes, **Back** to return to the list without making any changes
* Click **Previous** or **Next** to save the changes and go to the previous or next major respectively
* Click **Delete** to delete a major. Majors with an external ID (i.e., that has been imported from an external system) cannot be deleted.

### Edit Majors
Click **Edit** to edit all majors

![Majors](images/majors-4.png){:class='screenshot'}

* Use the ![Add](images/icon-add.png) icon to add a new line and ![Delete](images/icon-delete.png) to delete a line
* Majors with an external ID (i.e., that has been imported from an external system) cannot be deleted
* Click **Save** to make changes, **Back** to return to the list without making any changes

### Export CSV/PDF
Click the **Export CSV** or **Export PDF** to export the list of majors to a CSV or PDF document respectively