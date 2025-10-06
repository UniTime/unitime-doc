---
layout: manual
title: Student Scheduling Manual
updated: October 2025
warn: Work in progress!
---

### Table of Contents
{:.no_toc}
* table
{:toc}


# Introduction

Student scheduling, sometimes called *student sectioning*, involves assigning students to classes (course sections) based on their individual course demands. It consists of courses that have already been timetabled, students and their individual course demands, and producing a class schedule for each student. It is modeled as an assignment of student course requests with enrollments, i.e., valid combinations of classes that the student needs to take to enroll in a course. There are various hard constraints, such as students not having a time conflict (unless allowed, in which case the overlapping time is to be minimized), classes and courses being limited in size, or restrictions limiting who can attend a particular class or course. It is also an optimization problem, combining a long list of various criteria, such as maximizing the number
of courses each student gets, considering student and course priorities, student preferences, penalizing alternatives and substitutes, minimizing distance conflicts or travel times, etc. In the rest of this section, the most interesting aspects of the student scheduling problem are discussed.

### Course Structure
Each course may be offered in multiple configurations, such as face-to-face or online, each with multiple components (subparts), such as a lecture and a lab. Each subpart may contain multiple alternative classes. A student requesting a course will get one class of each subpart of a single configuration. There can be additional parent-child relations between individual classes, which also must be followed. So, for example, a student may get Lec 1 - Lab 1, Lec 1 - Lab 2, Lec 2 - Lab 3, or Lec 2 - Lab 4 class combination if attending the course face-to-face, or Dist 1 when attending the course online. Each class can also have a limit, allowing only a certain number of students to get in.

### Reservations and Restrictions
Access to courses or certain components of courses, such as configurations or individual classes, may be restricted with [reservations](../reservations). A reservation reserves a certain number of seats in the course, or some of its components, for a particular group of students, e.g., identified by their study program. A restriction does not reserve any space, but the students must follow it. For example, a student of an online program may be restricted to the online course configuration, while other students may freely choose between the two configurations, assuming space is available. Similarly, there can be 100 spaces in a course reserved for students of a Computer Science major, or the space in one of the Labs may be reserved for a particular cohort.

### Alternative and Substitute Courses
A student may provide alternatives to each course. The aim is to get a given number of courses, and one or more alternative courses can be provided for each course. It is also possible to provide substitute courses that can act as alternatives to any other course requests except those that have been marked as no-sub by the advisors (typically those that the student must take). The order in which the courses are requested is also important, as it helps us to break the ties, e.g., when it is not possible to get both courses because they are overlapping in time, or when there are more students requesting the course than the space available.

### Student Preferences and Requirements
A student can indicate which course configurations and/or classes are preferred for each course. It is also possible to provide free time requirements, which can act as unavailabilities (i.e., a student cannot get a class at the time) or preferences (i.e., an overlapping time with the free time should be minimized), depending on the position of the free time among the courses.

Students may also indicate whether they prefer online or face-to-face classes and whether back-to-backs are preferred or discouraged. For the Summer terms, which are organized into three four-week modules, it is also possible to indicate during which modules the student can have classes and whether they can attend classes on campus.

### Student and Course Request Priorities
Student and course request priorities have been added to help students graduate on time. First of all, advisors may indicate courses as vital to the student, which means that the student absolutely needs the course (or one of the provided alternatives) to progress towards their degree. Moreover, students are divided into priority students (such as athletes and students in university bands and orchestra), students near graduation (with 100 or more credits earned), senior students (60 or more credits), and the rest. Vital course requests take priority over student priorities.

### Batch vs Online
Student scheduling in UniTime can be done in two modes. In **batch** mode, the [Student Scheduling Solver](../student-scheduling-solver) is used to compute individual student schedules for all (or a selected population of) students simultaneously. This is an optimization process aimed at maximizing the number of courses students can take, as well as considering various optimization criteria, including travel times and the aforementioned preferences and priorities. This process includes a pre-registration step where students provide information about the courses they need, along with additional preferences, alternatives, and requests for free time.

The **online** student scheduling serves students as they come. They can use the [Student Scheduling Assistant](../student-scheduling-assistant) to either modify their existing schedule or create a new one from scratch (e.g., if only the online mode is used, or the student did not complete the batch for some reason).

The two modes are not mutually exclusive. Typically, the online mode is enabled once the students have been provided their initial schedule using the pre-registration & batch process. In this case, the students use the [Student Scheduling Assistant](../student-scheduling-assistant) to make changes to their schedule, and possibly wait-list for 
courses that are currently full.

### Student Scheduling Prerequisites
The student scheduling component requires that the course timetabling be already completed with the course timetabling solution(s) saved and committed. Additionally, it makes use of [Reservations](../reservations), the [Associated Course](../edit-course-offering#details) relations, and two [distribution preferences](../distribution-preferences):
* **Linked Classes**: Classes (of different courses) are to be attended by the same students. For instance, if class A1 (of course A) and class B1 (of course B) are linked, a student requesting both courses must attend A1 if and only if they also attend B1.
* **Ignore Student Conflicts**: All student conflicts between the given classes are to be ignored.

Besides the courses and the course timetable, the student scheduling also needs to have **students** imported, possibly with their course requests when the batch is used without doing [pre-registration](../student-course-requests) in UniTime. Students cannot be entered directly in UniTime; the expectation is that they will be imported from an external Student Information System. This can be done using the [Students XML](https://www.unitime.org/interface/studentInfoImport.xml) or the [Student Course Requests XML](https://www.unitime.org/interface/woebegonStudents.xml) format using the Administration > Academic Sessions > [Data Exchange](../data-exchange) page (see [XML Interfaces](https://www.unitime.org/uct_interfaces.php) for more details).

# Batch Student Scheduling

The batch student scheduling is done using the Students > [Batch Solver](../student-scheduling-solver) page. The student schedules are computed using the student course requests that can be either filled in by students in UniTime using the [Student Course Requests](../student-course-requests) page (see below) or imported using the Administration > Academic Sessions > [Data Exchange](../data-exchange) page using the [Student Course Requests XML](https://www.unitime.org/interface/woebegonStudents.xml) format (see [XML Interfaces](https://www.unitime.org/uct_interfaces.php) for more details).

To enable pre-registration, the [academic session](../academic-sessions) needs to be in a status that allows for Student Scheduling: Course Requests (see [Status Types](../status-types) for more details), the students need to exist in UniTime, and if an external authentication is used (such as [LDAP](../LDAP), [CAS](../CAS), or [OAuth2](../OAuth2)), their external IDs must match the user ID of the authenticated user. Such users will be granted the [Student role](../roles) upon logging in to UniTime and will have the related [permissions](../permissions). 

## Advisor Course Recommendations

It is possible to use UniTime for advising. Advisors can use the [Online Student Scheduling Dashboard](../online-student-scheduling-dashboard) to monitor their students' and their (pre-)registration progress. They can use the [Advisor Course Recommendations](../advisor-course-recommendations) page to change their status and provide a list of courses that they need to register for.

Please note that the [Advisor Course Recommendations](../advisor-course-recommendations) page is an optional component and does not need to be used for students to pre-register. And even when used, students still need to use the [Student Course Requests](../student-course-requests) page, which will get pre-populated with the advisor course recommendations, and need to **Submit** the page to complete their pre-registration.

![Advisor Course Recommendations](../images/advisor-course-recommendations-1.png){:class='screenshot'}

When opened, the advisor can look up a student, and the page gets pre-populated with the existing data. A different student can also be looked up by clicking the **Lookup Student** button or when the student's name or ID is clicked. If advisor course recommendations from multiple academic sessions can be viewed and/or edited, an academic session can be selected afterward. It can be changed at any time by clicking the term field. When there are any unsubmitted changes, the user is prompted when leaving the page or changing the student or session.

Just like on the [Student Course Requests](student-course-requests), the page automatically offers course suggestions as the course name is being typed in (but it is possible to put in free text too), fills in credits, counts the credit totals, etc. When submitted, there is a PDF version generated that can be printed and signed by the student. It is also possible to email the document to the student (with the advisor on CC) when the page is submitted (and the Send email confirmation toggle is checked). In this case, the Send email... dialog pops up after the form has been successfully submitted, and the user can provide an additional message and email address if needed.

The page also allows for a student status change when submitted. This eliminates the need for the advisor to also use the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard) to change the student status (e.g., to let the student fill in his/her course requests). UniTime keeps a record of these advisor course recommendations for possible auditing/reporting (what students requested versus what they have been advised, list students who have already been advised that did not fill their course requests in, etc.). Some of these can be seen on the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard).

### Settings
The student advisors can be defined on the Administration > Academic Sessions > [Student Advisors](../student-advisors) page. If an external authentication is used (such as [LDAP](../LDAP), [CAS](../CAS), or [OAuth2](../OAuth2)), their external IDs must match the user ID of the authenticated user. Such users will be granted the [Advisor role](../roles) upon logging in to UniTime and will have the related [permissions](../permissions). 

## Student Course Requests

Students can use the [Student Course Requests](../student-course-requests) page to fill in the courses they would like to get, together with their alternatives, substitutes, course preferences, and free time requests.

![Student Course Requests](../images/student-course-requests-1.png){:class='screenshot'}

The Student Course Requests page can be used to collect course requests (course pre-registrations) from students. It is a variant of the [Student Scheduling Assistant](../student-scheduling-assistant) page that is used during online scheduling, without the ability to create a student schedule right away. Course requests can be collected during the timetabling process, once it is known which courses will be offered. Once student course requests are collected, the [Student Sectioning Solver](../student-scheduling-solver) can be used to create an optimized schedule for all the students. After that, online student scheduling can be enabled, allowing students to use the [Student Scheduling Assistant](../student-scheduling-assistant) page to review their schedule and make any necessary modifications.

### Settings
If student statuses are being used (see Administration > Other > [Student Status Types](../student-scheduling-status-types)), the student's status must allow for **Registration** for the page to be available and **Student Register** to make changes. The default student status is set on the Administration > Academic Sessions > [Academic Sessions](../academic-sessions) page; individual student statuses can be set on the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard) or by advisors using the [Advisor Course Recommendations](../advisor-course-recommendations) page.

## Student Scheduling Solver

Once students have filled out their [student course requests](../student-course-requests) or the requests have been imported from an external system, the [Student Scheduling Solver](../student-scheduling-solver) page can be used to run the solver and produce individual student class schedules.

![Student Scheduling Solver](../images/student-scheduling-solver-1.png){:class='screenshot'}

There are the following properties that can be selected
* The **Solver Configuration** that is to be used
    * Solver configurations are defined on the Administration > Solver > [Configurations](../solver-configurations) page. Only configurations with the Student Scheduling Solver appearance are applicable for student scheduling and have the appropriate parameters available.
* The **Solver mode** indicates whether the solver should consider the existing assignments or not
    * If the **MPP** mode, standing for Minimal Perturbation Problem, is used, the solver will also try to minimize changes to the original timetable
    * The **Initial** mode does not minimize changes (it will still load the existing timetable if it exists)
    * The **Projection** mode can be used to optimize the location of the remaining space in the courses
        * This can be used, e.g., if only certain groups of students are being batched
        * The selected **Projected student course demands** (such as curricula or last-like enrollment) are loaded together with the course requests to fill in the remaining space; while the projected requests have much lower priority, the solver can use them to move students away from classes that will be needed for the students that come later (and, e.g., only using the online student scheduling).
* The **When finisher** option specifies an automatic operation when the solver run has finished
    * This option does not get used if the solver is stopped manually using the **Stop** button
* The **Student weights** parameter defines whether the order of the courses on the [Student Course Requests](../student-course-requests) page is used (the **Priority** option), or ignored with all courses being considered equally (the **Equal** option).
    * The **Equal** option is typically only used when requests are imported from an external system with no particular priority order.
* The **Student Filter** can be used to restrict the population of students that are to be loaded into the solver.
    * Other students who are already enrolled will still count toward the class, configuration, course, and reservation limits.
    * This allows for scheduling the students in phases or waves, or separately for each department.
    * The format of the Filter has the same format as the [Filter](../scheduling-dashboard-filter) on the [Online Student Scheduling Dashboard](../online-student-scheduling-dashboard) page, e.g., `area:A` or `major:M1 or major:M2` or `group:"My Students" and not major:M3`
* Additional parameters can be displayed, depending on the [Solver Parameters](../solver-parameters) defined.

The data can be loaded into the solver using the **Load** button, and the solver can be started using the **Start** button. When no data are loaded into the solver, using **Start** will first load the solver and then start it. This can be combined with the **When finished** parameter, for example, to save and unload the solver once it is done automatically.

The **Stop** button can stop a running solver, or it can be left running until it stops itself. The solver run is typically 8 hours, which can be adjusted with the other student scheduling solver parameters on the Administration > Solver > [Configurations](../solver-configurations) page. The solver works with two student schedules: the current one (displayed on other pages and manually changeable using the [Batch Student Solver Dashboard](../batch-student-solver-dashboard) page) and the best schedule that the solver uses to record the best solution it has seen during the search. To save the current student schedule, click the **Save** button. The solver can be unloaded from memory using the **Unload** button.

The **Clear** button will unassign all student schedules, allowing the solver to start from scratch, even when existing schedules have been loaded. It can also be used to unassign all student schedules in the database (delete the existing solution) by using the **Load**, **Clear**, and **Save** buttons in this order.

The **Reload Input Data** button can be used to reload the input data (courses with their structure, timetable, and reservations, student course requests) without losing the current student schedule. This will load everything into the solver, using the newly selected configuration, except for the saved student schedules. Afterward, the current student schedule will be reassigned to the newly loaded requests. This is particularly useful when changes have been made to the input data, eliminating the need to perform **Save**, **Unload**, and **Load** again. Please note that some requests may be left unassigned if their current assignment is incompatible with the changes made to the input data. Please check the solver warnings for any such cases once the reload is done.

The **Save To Best** and **Restore From Best** buttons at the bottom of the page can be used to copy the current schedule over to the best manually or vice versa.

## Published Runs

When test runs are enabled (the user has the *Student Sectioning Solver Publish* [permission](../permissions)), the **Publish** button (on the [Student Scheduling Solver](../student-scheduling-solver) page) can be used to save the solution under the [Published Schedule Runs](../published-schedule-runs) page without actually saving the student class enrollments in the database. This can be very useful for conducting periodic (e.g., nightly) test runs during pre-registration, without saving any student schedules in the database yet.

![Published Schedule Runs](../images/published-schedule-runs-1.png){:class='screenshot'}

There can be only one published solver run per academic session, but UniTime will retain a history of previously published runs. A published run can be visible to other users who have the permissions to see the [Student Sectioning Dashboard](../batch-student-solver-dashboard) and/or the [Published Schedule Runs](../published-schedule-runs) page.

A published solver run is visible to all users who have the Student Scheduling and Student Sectioning Solver Dashboard and/or Student Sectioning Solver Reports permissions (possibly including advisors, departmental schedule managers, and instructors). It is indicated in the solver status (below the page name) as 'Solver Published'. A published solver run is static (it is loaded in the solver, but cannot be started or modified using the Scheduling Assistant dialog on the dashboard).

It is possible to extend the **When finished** solver parameter to allow for `Publish` or `Publish and Unload` in the [Solver Configurations](../solver-configurations).

To Administration > Academic Sessions > [Task Scheduler](../task-scheduler) page can be used to schedule the periodic test runs using the [Student Scheduling: Start Test Run](https://github.com/UniTime/unitime/blob/master/Documentation/Scripts/Student%20Scheduling%20Start%20Test%20Run.xml) script. To register the script, download the linked XML and import it using the [Data Exchange](../data-exchange) page.

# Online Student Scheduling

*Work in progress...*

## Student Scheduling Assistant

## Re-Scheduling & Wait-Listing

# Administration

*Work in progress...*

## Student Statuses

## Student Scheduling Rules
