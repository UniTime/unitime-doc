---
layout: default
title: Concentrations
---


## Screen Description

The Concentrations screen displays and allows editing of the list of available major concentrations for the current academic session.

![Concentrations](images/concentrations-1.png){:class='screenshot'}

Major concentrations are one of the **optional** student curricular properties, typically used to express a further variants of a major. Each concentration belongs to a particular major. Student curriculum may contain the following items:

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

Each major concentration contains the following properties:

* External Id
	* External ID of the concentration
	* External IDs are only editable via the [XML import](https://www.unitime.org/uct_interfaces.php)
	* Concentrations with an external ID cannot be deleted. The presence of the External ID indicates that the concentration has been imported from an external system.

* Code
	* Abbreviation/Code of the concentration

* Name
	* Name of the concentration

* Major
	* Major to which the concentration belongs

## Operations

The table can be sorted by any of its columns, just by clicking on the column header and the sorting option that opens.

### Add Concentration
Click **Add** to add a new concentration

![Concentrations](images/concentrations-2.png){:class='screenshot'}

* Click **Save** to create a new concentration
* Click **Back** to return to the list without making any changes

### Edit Concentration
Click a particular concentration to make changes or to delete the concentration

![Concentrations](images/concentrations-3.png){:class='screenshot'}

* Click **Save** to make changes, **Back** to return to the list without making any changes
* Click **Previous** or **Next** to save the changes and go to the previous or next concentration respectively
* Click **Delete** to delete a concentration. Concentrations with an external ID (i.e., that has been imported from an external system) cannot be deleted.

### Edit Concentrations
Click **Edit** to edit all concentrations

![Concentrations](images/concentrations-4.png){:class='screenshot'}

* Use the ![Add](images/icon-add.png) icon to add a new line and ![Delete](images/icon-delete.png) to delete a line
* Concentrations with an external ID (i.e., that has been imported from an external system) cannot be deleted
* Click **Save** to make changes, **Back** to return to the list without making any changes

### Export CSV/PDF
Click the **Export CSV** or **Export PDF** to export the list of concentrations to a CSV or PDF document respectively