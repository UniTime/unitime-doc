---
layout: default
title: Data Exchange
---


## Screen Description

### Export


 Select type of data for export, check/uncheck the distribution options and click **Export**.


 The Data Import screen provides interface for importing data from XML files.


 Note: In most cases, the existing data (for the selected academic session) are replaced by the content of the given XML file.

## Details

### Import


 Type in the location of a file or click on **Browse** and select a file where the data is stored, then click on **Import**.


 The needed format is described at [http://www.unitime.org/uct_interfaces.php](http://www.unitime.org/uct_interfaces.php).


![Data Exchange](images/data-exchange-1.png){:class='screenshot'}

### Notes

* Buildings and rooms are imported as external buildings and rooms, you need to use Update Data operation on [Buildings](buildings) page (menu Administration > Academic Sessions > Buildings) for the buildings and rooms to show up in the application. Global room features need to be crated before this update, and their abbreviation must match the roomFeature.feature attribute.

* Staff is imported into the staff table, to pull in the instructors use Manage Instructor List operation on the [Instructors](instructors) page (menu Courses > Input Data > Instructors).
