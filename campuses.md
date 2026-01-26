---
layout: default
title: Campuses
---

## Screen Description

The Campuses screen displays and allows editing of the list of available campuses for the current academic session.

![Campuses](images/campuses-1.png){:class='screenshot'}

Campuses are one of the **optional** student curricular properties. Student curriculum may contain the following items:

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

Each campus contains the following properties:

* External Id
	* External ID of the campus
	* External IDs are only editable via the [XML import](xml)
	* Campuses with an external ID cannot be deleted. The presence of the External ID indicates that the campus has been imported from an external system.

* Abbreviation
	* Campus abbreviation

* Name
	* The name of the campuses

## Operations

The table can be sorted by any of its columns, just by clicking on the column header and the sorting option that opens.

### Add Campus
Click **Add** to add a new campus

![Campuses](images/campuses-2.png){:class='screenshot'}

* Click **Save** to create a new campus
* Click **Back** to return to the list without making any changes

### Edit Campus
Click a particular campus to make changes or to delete the campus

![Campuses](images/campuses-3.png){:class='screenshot'}

* Click **Save** to make changes, **Back** to return to the list without making any changes
* Click **Previous** or **Next** to save the changes and go to the previous or next campus respectively
* Click **Delete** to delete a campus. Campuses with an external ID (i.e., that has been imported from an external system) cannot be deleted.

### Edit Campuses
Click **Edit** to edit all campuses

![Campuses](images/campuses-4.png){:class='screenshot'}

* Use the ![Add](images/icon-add.png) icon to add a new line and ![Delete](images/icon-delete.png) to delete a line
* Campuses with an external ID (i.e., that has been imported from an external system) cannot be deleted
* Click **Save** to make changes, **Back** to return to the list without making any changes

### Export CSV/PDF
Click the **Export CSV** or **Export PDF** to export the list of campuses to a CSV or PDF document respectively