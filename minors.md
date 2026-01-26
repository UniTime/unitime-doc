---
layout: default
title: Minors
---


## Screen Description

The Minors screen displays and allows editing of the list of available minors for the current academic session.

![Minors](images/minors-1.png){:class='screenshot'}

Minor are one of the student curricular properties, typically used to express a secondary specialization. Each minor belongs to a particular academic area. Student curriculum may contain the following items:

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

Each minor contains the following properties:

* External Id
	* External ID of the minor
	* External IDs are only editable via the [XML import](xml)
	* Minors with an external ID cannot be deleted. The presence of the External ID indicates that the minor has been imported from an external system.

* Code
	* Abbreviation/Code of the minor

* Name
	* Name of the minor

* Academic Area
	* Academic area to which the minor belongs

## Operations

The table can be sorted by any of its columns, just by clicking on the column header and the sorting option that opens.

### Add Minor
Click **Add** to add a new minor

![Minors](images/minors-2.png){:class='screenshot'}

* Click **Save** to create a new minor
* Click **Back** to return to the list without making any changes

### Edit Minor
Click a particular minor to make changes or to delete the minor

![Minors](images/minors-3.png){:class='screenshot'}

* Click **Save** to make changes, **Back** to return to the list without making any changes
* Click **Previous** or **Next** to save the changes and go to the previous or next minor respectively
* Click **Delete** to delete a minor. Minors with an external ID (i.e., that has been imported from an external system) cannot be deleted.

### Edit Minors
Click **Edit** to edit all minors

![Minors](images/minors-4.png){:class='screenshot'}

* Use the ![Add](images/icon-add.png) icon to add a new line and ![Delete](images/icon-delete.png) to delete a line
* Minors with an external ID (i.e., that has been imported from an external system) cannot be deleted
* Click **Save** to make changes, **Back** to return to the list without making any changes

### Export CSV/PDF
Click the **Export CSV** or **Export PDF** to export the list of minors to a CSV or PDF document respectively