---
layout: default
title: Academic Classifications
---


## Screen Description

The Academic Classifications screen displays and allows editing of the list of available academic classifications for the current academic session.

![Academic Classifications](images/academic-classifications-1.png){:class='screenshot'}

Academic classifications are one of the student curricular properties, typically used to express the semester or year of study. Student curriculum may contain the following items:
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

Each academic classification contains the following properties:

* External Id
	* External ID of the academic classification
	* External IDs are only editable via the [XML import](https://www.unitime.org/uct_interfaces.php)
	* Academic classifications with an external ID cannot be deleted. The presence of the External ID indicates that the academic classification has been imported from an external system.

* Code
	* Abbreviation/Code of the academic classification

* Name
	* Name of the academic classification

## Operations

The table can be sorted by any of its columns, just by clicking on the column header and the sorting option that opens.

### Add Academic Classification
Click **Add** to add a new academic classification

![Academic Classifications](images/academic-classifications-2.png){:class='screenshot'}

* Click **Save** to create a new academic classification
* Click **Back** to return to the list without making any changes

### Edit Academic Classification
Click a particular academic classification to make changes or to delete the academic classification

![Academic Classifications](images/academic-classifications-3.png){:class='screenshot'}

* Click **Save** to make changes, **Back** to return to the list without making any changes
* Click **Previous** or **Next** to save the changes and go to the previous or next academic classification respectively
* Click **Delete** to delete an academic classification. Academic classifications with an external ID (i.e., that has been imported from an external system) cannot be deleted.

### Edit Academic Classifications
Click **Edit** to edit all academic classifications

![Academic Classifications](images/academic-classifications-4.png){:class='screenshot'}

* Use the ![Add](images/icon-add.png) icon to add a new line and ![Delete](images/icon-delete.png) to delete a line
* Academic classifications with an external ID (i.e., that has been imported from an external system) cannot be deleted
* Click **Save** to make changes, **Back** to return to the list without making any changes

### Export CSV/PDF
Click the **Export CSV** or **Export PDF** to export the list of academic classifications to a CSV or PDF document respectively