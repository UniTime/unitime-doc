---
layout: default
title: Student Conflicts
---



 The prevention of student conflicts is one of the main driving forces for the solver when creating a timetable. The solver takes students demands and/or information about last like-semester student enrollments and optimizes the timetable so that the students can take maximum of courses they want (supposing that the students sign up for courses and are scheduled into classes - for example, a student signs up for BIOL 110 and is assigned one of the lectures and one of the labs - the student cannot pick which lecture/laboratory it should be).


 The number of student conflicts is a (weighted) number of students who want two particular courses but cannot take them because there is no feasible combination of classes (for example, all lectures of one course overlap with labs of the other course). The most accurate numbers are reached when timetables for all departments are loaded together into the solver.
