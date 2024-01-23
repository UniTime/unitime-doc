---
layout: default
title: Exam Naming Convention
---



 An exam is named by the object that is having the exam (section, config, course, offering). E.g., if a course MGMT 200 is having an exam, it is named **MGMT 200**, an exam for a class A&AE 203 Lec 1 will be named **A&AE 203 Lec 1**.


 In the case of an exam that links multiple classes, courses etc. together, it contains a comma (or semicolon) separated list of the names of all objects that are having the exam, in the order of these objects that we are using through the Timetabling application. Also, it is trying to skip parts (subject area, course number and instructional type) that are in common.


 So, for instance,

* if there is an exam for labs 1, 3, 19 and 29 of course EPCS 101, the exam is named **EPCS 101 Lab 1, 3, 19, 29**.

* An exam for classes MA 161 Lec 1 and 2, and MA 161E Lec 1 is named **MA 161 Lec 1, 2; 161E Lec 1**.

* And exam for courses MA 416 and STAT 416 is named **MA 416; STAT 416**


 It is also possible to rename an exam if needed.

## Customization

### Codes


 Following codes can be used in exam names:


 %s


 subject area abbreviation


 %c


 course number


 %i


 instructional type abbreviation (e.g., Lec, Rec)


 %n


 section number (including suffix, e.g., **1a** for ENGL 106 Lec 1a)


 %x


 configuration name


 %d


 department abbreviation


 %D


 department code


 %a


 class suffix (aka div-sec number)


 %y


 instructional type suffix (e.g., **a** for ENGL 106 Lec 1a)


 %e


 class extended id


 %f


 course extended id


 %o


 offering extended id


 %t


 exam type suffix (using application properties tmtbl.exam.name.type.Final and tmtbl.exam.name.type.Midterm)


 %I


 instructional type code


 %p


 instructional type parent abbreviation (e.g., **Lec** for Lec, Lec 1, or Lec 2)


 %P


 instructional type parent parent code


 %_


 space

### Properties


 All objects (classes, courses, etc.) that are associated with an exam are iterated ordered by subject area, course number, classes and their position within the course. For each of these objects a name is appended into the examination name using the following patterns.


 tmtbl.exam.name.Course


 course offering name


 tmtbl.exam.name.Offering


 instructional offering name


 tmtbl.exam.name.Config


 instructional offering configuration name


 tmtbl.exam.name.Class


 class name


 tmtbl.exam.name.suffix


 suffix (to be appended at the end of an examination name, e.g. %_%t)


 tmtbl.exam.name.sameSubject.Course


 course offering name (if the previously iterated object was of the same subject area)


 tmtbl.exam.name.sameSubject.Offering


 instructional offering name (if the previously iterated object was of the same subject area)


 tmtbl.exam.name.sameSubject.Config


 instructional offering configuration name (if the previously iterated object was of the same subject area)


 tmtbl.exam.name.sameSubject.Class


 class name (if the previously iterated object was of the same subject area)


 tmtbl.exam.name.sameCourse.Config


 instructional offering configuration name (if the previously iterated object was an instructional offering configuration of the same instructional offering)


 tmtbl.exam.name.sameCourse.Class


 class name (if the previously iterated object was a class of the same instructional offering, but different scheduling subpart)


 tmtbl.exam.name.sameSubpart.Class


 class name (if the previously iterated object was a class of the same scheduling subpart)


 tmtbl.exam.name.diffSubject.separator


 separator between two objects of different subject area


 Additional properties are used for generation of an examination name:


 tmtbl.exam.name.maxLength


 maximal length of an examination name (if the name is too long, it is cut before the suffix and **...** are attached at the end)


 tmtbl.exam.name.type.Final


 string that is to be printed for **%t** when for a final exam


 tmtbl.exam.name.type.Midterm


 string that is to be printed for **%t** when for an midterm exam

### Defaults


 Default settings (that corresponds with the naming convention described at the beginning of this document):
```
tmtbl.exam.name.maxLength=100
tmtbl.exam.name.Course=%s %c
tmtbl.exam.name.Offering=%s %c
tmtbl.exam.name.Config=%s %c [%x]
tmtbl.exam.name.Class=%s %c %i %n
tmtbl.exam.name.suffix=
tmtbl.exam.name.sameSubject.Course=; %c
tmtbl.exam.name.sameSubject.Offering=; %c
tmtbl.exam.name.sameSubject.Config=; %c [%x]
tmtbl.exam.name.sameSubject.Class=; %c %i %n
tmtbl.exam.name.sameCourse.Config=, [%x]
tmtbl.exam.name.sameCourse.Class=, %i %n
tmtbl.exam.name.sameSubpart.Class=, %n
tmtbl.exam.name.diffSubject.separator=;%_
tmtbl.exam.name.type.Final=
tmtbl.exam.name.type.Midterm=(t)
```
