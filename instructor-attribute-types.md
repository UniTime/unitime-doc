---
layout: default
title: Instructor Attribute Types
---


## Screen Description

This page defines instructor attribute types (every instructor attribute must have a type). Instructor attribute types are used to categorize instructor attributes. Instructor attribute types are academic session independent (the same set is used across all academic sessions). The user needs to have Instructor Attribute Types permission to be able to see the instructor attribute types. The permission Instructor Attribute Type Edit is needed to make modifications.

## Details

Each attribute type has an abbreviation, a name, and two toggles:

* **Conjunctive**: if two or more attributes of the same conjunctive type are required on a teaching request, this means that only instructors that have ALL the indicated required attributes can be used (same as with room features). If the attribute type is disjunctive (conjunctive toggle is unchecked), it is sufficient for the instructor to have just one of the required attributes of the given type (same as with room groups).

* **Required Attribute**: If a teaching request has a preference of an attribute that is of the required attribute type (unless the preference is prohibited), the preference is considered as required and the actual preference is used to compare two instructors.

For example, if a teaching request strongly prefers Organic Chemistry Skill and prefers Inorganic Chemistry Skill (assuming that the Skill is a required disjunctive attribute type), an instructor must have either Organic Chemistry Skill or Inorganic Chemistry Skill (because of the required attribute type). Among these, instructors with both skills are most preferred, after which instructors with only the Organic Chemistry Skill are preferred before instructors with only the Inorganic Chemistry Skill (because of the strongly preferred preference on the Organic Chemistry Skill).

If the Skill attribute type is not marked as required attribute, instructors without the above two skills can also teach the course but are less preferred than instructors with one or both of the above two skills.

## Operations

To edit or delete an attribute type, click on the appropriate line, [Edit Instructor Attribute Type](edit-instructor-attribute-type) page will appear. All the attribute types can be edited on the [Edit Instructor Attribute Types](edit-instructor-attribute-types) page. To do so, click on the **Edit** button. Only attribute types that are not being used can be deleted.

A new attribute type can be added on the [Edit Instructor Attribute Types](edit-instructor-attribute-types) page (button **Edit**) or using [Add Instructor Attribute Type](add-instructor-attribute-type) page (button **Add**).

The table can be ordered by any of the columns. To do so, click on the column header and select Sort by <column name> option.


![Instructor Attribute Types](images/instructor-attribute-types-1.png){:class='screenshot'}
