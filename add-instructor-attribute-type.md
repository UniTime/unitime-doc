---
layout: default
title: Add Instructor Attribute Type
---


## Screen Description


 The Add Instructor Attribute Type can be used to create a new attribute type. Instructor attribute types are used to categorize instructor attributes. The user needs to have Instructor Attribute Type Edit permission to be able to create a new instructor attribute type. See [Instructor Attribute Types](instructor-attribute-types) for more details.

## Details


 Each attribute type has an abbreviation, a name, and two toggles:

* **Conjunctive**: if two or more attributes of the same conjunctive type are required on a teaching request, this means that only instructors that have ALL the indicated required attributes can be used (same as with room features). If the attribute type is disjunctive (conjunctive toggle is unchecked), it is sufficient for the instructor to have just one of the required attributes of the given type (same as with room groups).

* **Required Attribute**: If a teaching request has a preference of an attribute that is of the required attribute type (unless the preference is prohibited), the preference is considered as required and the actual preference is used to compare two instructors.


 For example, if a teaching request strongly prefers Organic Chemistry Skill and prefers Inorganic Chemistry Skill (assuming that the Skill is a required disjunctive attribute type), an instructor must have either Organic Chemistry Skill or Inorganic Chemistry Skill (because of the required attribute type). Among these, instructors with both skills are most preferred, after which instructors with only the Organic Chemistry Skill are preferred before instructors with only the Inorganic Chemistry Skill (because of the strongly preferred preference on the Organic Chemistry Skill).


 If the Skill attribute type is not marked as required attribute, instructors without the above two skills can also teach the course but are less preferred than instructors with one or both of the above two skills

## Operations


 Click **Save** to create the new attribute type. The button **Back** will get you back to [Instructor Attribute Types](instructor-attribute-types) page without creating any new attribute types.


![Add Instructor Attribute Type](images/add-instructor-attribute-type-1.png){:class='screenshot'}
