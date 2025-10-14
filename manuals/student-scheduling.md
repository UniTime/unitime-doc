---
layout: manual
title: Student Scheduling Manual
updated: October 2025
---

### Table of Contents
{:.no_toc}
* table
{:toc}


# Introduction

Student scheduling, sometimes called *student sectioning*, involves assigning students to classes (course sections) based on their individual course demands. It consists of courses that have already been timetabled, students and their individual course demands, and producing a class schedule for each student. It is modeled as an assignment of student course requests with enrollments, i.e., valid combinations of classes that the student needs to take to enroll in a course. There are various hard constraints, such as students not having a time conflict (unless allowed, in which case the overlapping time is to be minimized), classes and courses being limited in size, or restrictions limiting who can attend a particular class or course. It is also an optimization problem, combining a long list of various criteria, such as maximizing the number
of courses each student gets, considering student and course priorities, student preferences, penalizing alternatives and substitutes, minimizing distance conflicts or travel times, etc. In the rest of this section, the most interesting aspects of the student scheduling problem are discussed.

### Course Structure
Each course may be offered in multiple [configurations](../instructional-offering-configuration), such as face-to-face or online, each with multiple components (subparts), such as a lecture and a lab. Each subpart may contain multiple alternative classes. A student requesting a course will get one class of each subpart of a single configuration. There can be additional parent-child relations between individual classes, which also must be followed. So, for example, a student may get Lec 1 - Lab 1, Lec 1 - Lab 2, Lec 2 - Lab 3, or Lec 2 - Lab 4 class combination if attending the course face-to-face, or Dist 1 when attending the course online. Each class can also have a limit, allowing only a certain number of students to get in.

### Reservations and Restrictions
Access to courses or certain components of courses, such as configurations or individual classes, may be restricted with [reservations](../reservations). A reservation reserves a certain number of seats in the course, or some of its components, for a particular group of students, e.g., identified by their study program. A restriction does not reserve any space, but the students must follow it. For example, a student of an online program may be restricted to the online course configuration, while other students may freely choose between the two configurations, assuming space is available. Similarly, there can be 100 spaces in a course reserved for students of a Computer Science major, or the space in one of the Labs may be reserved for a particular cohort.

### Alternative and Substitute Courses
A student may provide alternatives to each course. The aim is to get a given number of courses, and one or more alternative courses can be provided for each course. It is also possible to provide substitute courses that can act as alternatives to any other course requests except those that have been marked as no-sub by the advisors (typically those that the student must take). The order in which the courses are requested is also important, as it helps us to break the ties, e.g., when it is not possible to get both courses because they are overlapping in time, or when there are more students requesting the course than the space available.

### Student Preferences and Requirements
A student can indicate which course configurations and/or classes are preferred for each course. It is also possible to provide free time requirements, which can act as unavailabilities (i.e., a student cannot get a class at the time) or preferences (i.e., an overlapping time with the free time should be minimized), depending on the position of the free time among the courses.

Students may also indicate whether they prefer online or face-to-face classes and whether back-to-backs are preferred or discouraged. For the Summer terms, which are organized into three four-week modules, it is also possible to indicate during which modules the student can have classes and whether they can attend classes on campus.

### Student and Course Request Priorities
Student and course request priorities have been added to help students graduate on time and to deal with popular courses of limited capacity. First of all, advisors may indicate courses as vital to the student, which means that the student absolutely needs the course (or one of the provided alternatives) to progress towards their degree. Moreover, students are divided into priority students (such as athletes and students in university bands and orchestra), students near graduation (with 100 or more credits earned), senior students (60 or more credits), and the rest. Vital course requests take priority over student priorities.

### Batch vs Online
Student scheduling in UniTime can be done in two modes. In **batch** mode, the [Student Scheduling Solver](../student-scheduling-solver) is used to compute individual student schedules for all (or a selected population of) students simultaneously. This is an optimization process aimed at maximizing the number of courses students can take, as well as considering various optimization criteria, including travel times and the aforementioned preferences and priorities. This process includes a pre-registration step where students provide information about the courses they need (usig [Student Course Requests](../student-course-requests)), along with additional preferences, alternatives, and requests for free time.

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

It is possible to use UniTime for advising. Advisors can use the [Online Student Scheduling Dashboard](../online-student-scheduling-dashboard) to monitor their students' and their (pre-)registration progress. They can use the [Advisor Course Recommendations](../advisor-course-recommendations) page to change their students' status and provide a list of courses that they need to register for.

Please note that the [Advisor Course Recommendations](../advisor-course-recommendations) page is an optional component and does not need to be used for students to pre-register. And even when used, students still need to use the [Student Course Requests](../student-course-requests) page, which will get pre-populated with the advisor course recommendations, and need to **Submit** the page to complete their pre-registration.

![Advisor Course Recommendations](../images/advisor-course-recommendations-1.png){:class='screenshot'}

When opened, the advisor can look up a student, and the page gets pre-populated with the existing data. A different student can also be looked up by clicking the **Lookup Student** button or when the student's name or ID is clicked. If advisor course recommendations from multiple academic sessions can be viewed and/or edited, an academic session can be selected afterward. It can be changed at any time by clicking the term field. When there are any unsubmitted changes, the user is prompted when leaving the page or changing the student or session.

The page automatically offers course suggestions as the course name is being typed in (but it is possible to put in free text too), fills in credits, counts the credit totals, etc. When submitted, there is a PDF version generated that can be printed and signed by the student. It is also possible to email the document to the student (with the advisor on CC) when the page is submitted (and the Send email confirmation toggle is checked). In this case, the Send email... dialog pops up after the form has been successfully submitted, and the user can provide an additional message and email address if needed.

The page also allows for a student status change when submitted. This eliminates the need for the advisor to also use the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard) to change the student status (e.g., to let the student fill in his/her course requests). UniTime keeps a record of these advisor course recommendations for possible auditing/reporting (what students requested versus what they have been advised, list students who have already been advised that did not fill their course requests in, etc.). Some of these can be seen on the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard).

### Recommendation Settings
The student advisors can be defined on the Administration > Academic Sessions > [Student Advisors](../student-advisors) page. If an external authentication is used (such as [LDAP](../LDAP), [CAS](../CAS), or [OAuth2](../OAuth2)), their external IDs must match the user ID of the authenticated user. Such users will be granted the [Advisor role](../roles) upon logging in to UniTime and will have the related [permissions](../permissions). 

The page requires the *Advisor Course Requests* permission. A user (typically an advisor) can look up and see advisor recommendations for all students; he/she may be only allowed to edit no students, only his/her students, or all students (depending on the *Student Scheduling Advisor Can Modify All Students* or *Student Scheduling Advisor Can Modify My Students* permissions).

The following additional flags can be provided by the advisor (for each course request) when enabled:

* Course Priority: **Critical**, **Important**, or **Vital**
    * Courses of elevated priority take precedence before other courses in the solver
    * See the `unitime.acrf.setCriticalCourses` configuration setting on the [Application Configuration](../application-configuration) screen

* Wait-Listing: **No-Sub** or **Wait-List**
    * *No-Sub* indicates that a course cannot be replaced by a substitute course
    * *Wait-List* indicates that the course cannot be replaced by a substitute course and will be wait-listed when the student cannot get in during the batch
    * See the `unitime.acr.waitlist` configuration setting on the [Application Configuration](../application-configuration) screen


## Student Course Requests

Students can use the [Student Course Requests](../student-course-requests) page to fill in the courses they would like to get, together with their alternatives, substitutes, course preferences, and free time requests.

![Student Course Requests](../images/student-course-requests-1.png){:class='screenshot'}

The Student Course Requests page can be used to collect course requests (course pre-registrations) from students. It is a variant of the [Student Scheduling Assistant](../student-scheduling-assistant) page that is used during online scheduling, without the ability to create a student schedule right away. Course requests can be collected during the timetabling process, once it is known which courses will be offered. Once student course requests are collected, the [Student Sectioning Solver](../student-scheduling-solver) can be used to create an optimized schedule for all the students. After that, online student scheduling can be enabled, allowing students to use the [Student Scheduling Assistant](../student-scheduling-assistant) page to review their schedule and make any necessary modifications.

A student may request one or more courses, ordered by their priority. Each course may include any number of alternatives. Preferences can be set on individual classes and/or for [instructional method](../instructional-methods) when the course has multiple configurations with different methods (e.g., Face-to-Face and Online). The student may also mark the class and instructional method preferences as required. This is not enabled by default as it effectively restricts the list of available enrollments into the course to those that include the class(es) or instructional method(s) that are marked as required. It is possible to type in the course name or part of its title directly into the page and use the available suggestions to find the matching course, or click the ![Course Finder](../images/icon-finder.png) icon to open the [Course Finder](../course-finder) dialog. Please note that on the [Course Finder](../course-finder) dialog, the *List of Classes* is only available, and the preferences can be set only after the course timetable has been published.

Free time requirements can also be put in the **Course Requests** table. They can be either typed in (day or days of the week + start time + end time) or selected using the [Course Finder](../course-finder) dialog by clicking the ![Course Finder](../images/icon-finder.png) icon. The position of a free time request is quite important. Any courses below the free time cannot overlap with the free time (the free time has higher priority), while courses above the free time are allowed to overlap. The solver will try to minimize the overlapping time in this case.

Additional substitute courses can be entered in the **Substitute Course Requests** table at the bottom of the page. Unlike with alternatives, the substitute course (possibly also with alternatives provided) can substitute any of the above courses to ensure the student will get the desired number of courses. Only courses that are marked with the Wait-List or No-Sub toggle (when allowed) cannot be substituted.

The **Preferences** button allows students to indicate their preference for class modality (face-to-face or online) and schedule gaps (prefer or avoid back-to-back classes).

### Course Requests Settings
In order for students to have access to the [Student Course Requests](../student-course-requests), the *Student* role needs to have *Student Scheduling Can Register* [permission](../permissions). The *Student Scheduling Can Require Preferences* permission is needed to be able to mark class and instructional method preferences as required.

If student statuses are being used (see Administration > Other > [Student Status Types](../student-scheduling-status-types)), the student's status must allow for **Registration** for the page to be available and **Student Register** to make changes. The default student status is set on the Administration > Academic Sessions > [Academic Sessions](../academic-sessions) page; individual student statuses can be set on the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard) or by advisors using the [Advisor Course Recommendations](../advisor-course-recommendations) page.

Students may or may not have the ability to indicate that a course can be wait-listed when it is not available (assuming that the course in question allows for wait-listing), or not replaced by a substitute (No-Sub). The ability to indicate the desire to wait-list a course is included in the [student scheduling status](../student-scheduling-status-types). A wait-listed or no-sub course cannot be replaced by a substitute course; however, alternative courses are possible.

Courses of a particular [Course Type](../course-types) can be made unavailable for students to select on the [Student Course Requests](../student-course-requests) page, when the appropriate course type is not allowed on the [student scheduling status](../student-scheduling-status-types). Such a course does not show up in the [Course Finder](../course-finder) dialog. Courses controlled by a [department](../departments) that does not have **Student Scheduling** enabled will also not be available for the students to find and select. This can be further adjusted using the [Student Scheduling Rules](../student-scheduling-rules).

The available options on the **Student Scheduling Preferences** dialog can be adjusted by various `unitime.enrollment.studentPrefs.*` parameters on the [Application Configuration](../application-configuration) page. Namely:

![Student Preferences](../images/student-scheduling-assistant-5.png){:class='screenshot'}

* Set `unitime.enrollment.studentPrefs.enabled` to enable or disable student preferences dialog (defaults to true, **Preference** button will not show when disabled)
* Set `unitime.enrollment.studentPrefs.datesAllowed` to `true` to allow for selection of the start and/or end dates. This is typically only enabled for Summer terms, as all automatically scheduled classes must fall into the selected dates.
* Set `unitime.enrollment.studentPrefs.reqOnlineAllowed` to `true` to allow students to Require Online as their class modality. This is typically only enabled for Summer terms as all automatically scheduled classes would have to be online (be arranged hours with no required room, have no room, or have only a pseudo room that does not check for room conflicts).
* Set `unitime.enrollment.studentPrefs.customNote` to a custom message (HTML format) to be displayed in the dialog.

When `unitime.sectioning.alternativeCourse` is set to `true`, the [Edit Course Offering](../edit-course-offering) page can be used to provide a **Default Alternative Course Offering** for a course that will be used when the student requests the course without providing any alternatives.

A custom course request validation can be implemented using the [CourseRequestsValidationProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/CourseRequestsValidationProvider.java) interface. This interface also provides an API for checking a student's eligibility to submit their course requests. This is used at Purdue University to check the student's ability to register for the selected courses and to request overrides for any potential registration errors. For example, please see the Purdue-specific [UniTime Course Requests User Manual](course-requests-purdue)

[Page access control](../access-statistics#access-control) is available for the page. It can be configured using the following properties:
* `unitime.accessControl.sectioning.activeLimitInMinutes`
    * Number of minutes of inactivity for the user to get the Inactive Warning.
    * Defaults to 15 minutes.
* `unitime.accessControl.sectioning.maxActiveUsers`
    * Maximal number of users using the page at the same time (not set or zero for disabled).
    * Not set by default.

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

### Solver Configuration

Optimization weights and other parameters can be adjusted on the Administration > Solver > [Configurations](../solver-configurations) page. Student scheduling solver configurations have the **Student Scheduling Solver** appearance.

The solver is working with variables (one variable is a requested course or free time, including its alternatives) and values (one value is a valid combination of sections for the course or its alternative). Besides of hard constraints that cannot be violated (class/configuration/course limits, time conflicts, reservations, linked sections, availability for students with teaching assignments, etc.), the batch solver tries to maximize the weighted sum of all assigned variables (course/free-time requests). The weight is computed using the request priority, the alternativity of the course in the request (1st alternative has a lower weight than the main course, etc.), distance conflicts and time overlaps (when allowed), and section and instructional method preferences. There are also additional penalties for classes that are without a time assignment, to promote section balancing, minimize changes (in MPP mode), and to keep students of the same group together. The solver can also consider last-like student demands or curricula to ensure that students avoid sections that are expected to be needed by students who have yet to arrive. These projected demands can be also used to compute expectations for the online student scheduling solver (which considers a few more weights, namely avoiding over-expected sections, considering current selection and locked sections, etc.).

The base weights for the priority-based weighting (course priorities are considered) are 0.501 for the first priority course, 0.251 for the second priority course, 0.126 for the third priority course, etc. (using 0.501^n, where n is 0, 1, 2, ...). So, getting the first priority and nothing else has a slightly higher weight than all the other courses. However, the alternatives are also factored in using the 0.501 factor, so the 1st alternative of the 1st priority course has the same weight as the 2nd priority course, etc.

As for the other weights, the time conflict can eat up to 1/2 of the weight of the lower priority course, proportional to how much time is being overlapped.

The following weights are much lower, mostly to provide order to the available enrollments:
- Each distance conflict takes 5% of the weight of the lower priority course (20% for the students that require short distances, see [Student Accommodations](../student-accommodations)).
- An enrollment without time assignment(s) is also penalized by deducting up to 1% of its weight (proportional to how many sections have no time assigned).
- There is up to a 0.5% penalty for section balancing
- Up to 10% for the distance to the original assignment (when MPP mode is used, penalizing a different time more than a different room)
- Up to 10% for the preferences (e.g., penalizing enrollment in a section that is not preferred, if there is a preference)
- Up to 10% for keeping students in the same group (for groups of [Student Group Type](../student-group-types) that have the *Keep Students Together* flag set)

Free time requests also play a role. If a course is below a free time request (in the priority), it cannot overlap with the free time. If it is above the free time request, the time conflicting with the free time is considered (in the same way as a time conflict between two courses).

Teaching assignments can prohibit time overlaps (a student cannot enroll in a class that overlaps with their time assignment) or minimize time overlaps (there is a penalty for overlapping time with a teaching assignment). When the [instructor scheduling](instructor-scheduling) module of UniTime is used to assign teaching assistants, this can be configured for each assignment (e.g., a TA must be available for the sections they are teaching, but may have a time conflict during the lecture).

The solver does not guarantee that it will just maximize the course request priority. The requests may be prioritized one level lower due to other penalties (especially those lower on the list, where time and distance conflicts can play a bigger role), but typically not more.

Vital (critical) course requests (and possibly also priority students) are handled by assigning them first and not allowing the solver to make a change that would favor a course request that is not critical over a critical one (despite their priorities). There are no additional weights associated with these. Moving the priority course requests to the top of the list of requested courses also helps the solver to ensure it gets as many of those assigned as possible.

### Student Priority

It is possible to prioritize some students over others. There can be six priority groups (Priority, Senior, Junior, Sophomore, Freshmen, and Normal). Students can be assigned to a particular priority group (other than Normal) via the [student groups](../student-groups) feature. So, for instance, a Priority group can be created for students who should be assigned first. For the solver to recognize the groups, there needs to be an appropriate solver parameter created (Administration > Solver > [Parameters](../solver-parameters) page, e.g., `Load.PriorityStudentFilter` for priority students, `Load.SeniorStudentFilter` for senior students, etc.) and populated with a student filter that would match the students that should have that priority. Here is an example of Priority group matching the `Load.PriorityStudentFilter`. 

![Priority Student Group](images/student-scheduling-1.png){:class='screenshot' style='max-width:600px;'}

### Student Schedule Quality

Starting with UniTime 4.4, additional student schedule quality criteria have been introduced in the student scheduling solver. These include:
- **Lunch Breaks** (allow time for lunch): there is a lunch conflict created when the student has two classes on a day that overlap with the lunch period of 11 am - 1 pm, with less than 30 minutes in between
- **Travel Time**: there is a conflict proportional to the travel time (in minutes) between two classes on the same day that are less than 1 hour apart (or less than 2 hours apart when the travel time is longer than the break time of the first class)
- **Back-to-Back**: there is a (negatively weighted) conflict for any two classes that are back-to-back and on the same day (the idea is to minimize gaps, so we want more classes clustered together)
- **Workday**: there is a conflict when the student has two classes that have more than six hours between the start of the first one and the end of the second one; the conflict is proportional to the number of hours over this limit (e.g., if the two classes span 8 hours, the penalty is 2) -- again the idea is to make the schedule more compact, without unnecessary gaps
- **Too Early**: there is a conflict when the class starts before 8:30 am (proportional to the time of the class before 8:30)
- **Too Late**: there is a conflict when the class ends after 5:30 pm (proportional to the time of the class after 5:30)

All these can be configured using the solver parameters using the [Solver Configurations](../solver-configurations) page.

## Published Runs

When test runs are enabled (the user has the *Student Sectioning Solver Publish* [permission](../permissions)), the **Publish** button (on the [Student Scheduling Solver](../student-scheduling-solver) page) can be used to save the solution under the [Published Schedule Runs](../published-schedule-runs) page without actually saving the student class enrollments in the database. This can be very useful for conducting periodic (e.g., nightly) test runs during pre-registration, without saving any student schedules in the database yet.

![Published Schedule Runs](../images/published-schedule-runs-1.png){:class='screenshot'}

There can be only one published solver run per academic session, but UniTime will retain a history of previously published runs. A published run can be visible to other users who have the permissions to see the [Student Sectioning Dashboard](../batch-student-solver-dashboard) and/or the [Published Schedule Runs](../published-schedule-runs) page.

A published solver run is visible to all users who have the Student Scheduling and Student Sectioning Solver Dashboard and/or Student Sectioning Solver Reports permissions (possibly including advisors, departmental schedule managers, and instructors). It is indicated in the solver status (below the page name) as 'Solver Published'. A published solver run is static (it is loaded in the solver, but cannot be started or modified using the Scheduling Assistant dialog on the dashboard).

It is possible to extend the **When finished** solver parameter to allow for `Publish` or `Publish and Unload` in the [Solver Configurations](../solver-configurations).

To Administration > Academic Sessions > [Task Scheduler](../task-scheduler) page can be used to schedule the periodic test runs using the [Student Scheduling: Start Test Run](https://github.com/UniTime/unitime/blob/master/Documentation/Scripts/Student%20Scheduling%20Start%20Test%20Run.xml) script. To register the script, download the linked XML and import it using the [Data Exchange](../data-exchange) page.

## Solver Dashboard

The Students > [Solver Dashboard](../batch-student-solver-dashboard) page can be used to check the solver results.

![Batch Student Solver Dashboard](../images/batch-student-solver-dashboard-1.png){:class='screenshot'}

When a solver run has been published, all personnel with the *Student Sectioning Solver Dashboard* [permission](../permissions) can use the page to see the results of the solver run that has been just published. This is particularly useful for the Schedule Managers to check which courses do not have enough space offered (zero *Available* space with students in the *Not-Enrolled* column), create time conflicts or have some reservations that are preventing students from getting in (there is still some space *Available* in the course, but still there are *Not-Enrolled* students). Similarly, the Advisors can use the page to check if their students are able to get the courses they need.

For the user that has the solver loaded in memory (just below the page name, the solver status says *Awaiting commands ...* instead of *Solver Published*), the [Batch Student Solver Dashboard](../batch-student-solver-dashboard) page can be used to make manual schedule adjustments to individual students. To do so, on the **Students** tab, click on the student and then click the **Scheduling Assistant** button. While it is not possible to make changes to a published solution, an administrative user can load a published solution into the solver (on the [Published Schedule Runs](../published-schedule-runs) page click on the **Load** button) and publish it again once done (on the [Student Scheduling Solver](../student-scheduling-solver) page click on the **Publish** button).

The Students > [Online Scheduling Dashboard](../online-student-scheduling-dashboard) can be used to monitor student pre-registrations (before a student scheduling solver has been saved) or the resulting student schedules (once a student scheduling solution has been saved). It is important to note the difference between these two dashboards, while they look similar (some features are only available in one or the other), they are populated by different data (loaded in the solver or saved in the database).

For more details about the dashboard, please see the [Student Scheduling Dashboard Manual](scheduling-dashboard).

## Solver Reports

There is a set of solver-computed reports available on the Students > [Solver Reports](../batch-student-solver-reports) page. The page can be used to compute reports from the current student scheduling solver solution that is loaded in the solver, or from the published solution. The *Student Sectioning Solver Reports* [permission](../permissions) is needed to access this page.

![Batch Student Solver Reports](../images/batch-student-solver-reports-1.png){:class='screenshot'}

There are many reports, concentrating on various aspects of the student scheduling optimization and results, like time conflicts, availability conflicts, distance conflicts, section balancing, or unused reservations.

# Online Student Scheduling

During the online student scheduling, the students use the [Student Scheduling Assistant](../student-scheduling-assistant) to build their class schedule or make schedule changes. The [Online Student Scheduling Dashboard](../online-student-scheduling-dashboard) can be used to monitor student progress. Advising and the [Advisor Course Recommendations](../advisor-course-recommendations) page can still be used, though it has been primarily designed for pre-registration.

To enable the online student scheduling, the [academic session](../academic-sessions) needs to be in a status that allows for *Online Scheduling* (in the *Student Scheduling* section, see Administration > Other > [Status Types](../status-types) for more details). Once the academic session status is changed, all the necessary data will be loaded into the *Online Scheduling Server*, allowing for prompt responses even when the [Student Scheduling Assistant](../student-scheduling-assistant) page is used by hundreds of students at the same time. The admin can monitor the online scheduling servers on the Administration > Solver > [Manage Solvers](../manage-solvers) page.

## Student Scheduling Assistant

The [Student Scheduling Assistant](../student-scheduling-assistant) helps students build a workable class schedule.  It takes a list of courses a student is interested in and determines the class sections the student needs to take in order to get as many of the courses being requested as possible.

![Student Scheduling Assistant](../images/student-scheduling-assistant-4.png){:class='screenshot'}

The Student Scheduling Assistant tries to calculate a schedule for the student based on the following criteria:

* the student’s priority for the course
* the student’s free time requests
* the student must be able to attend all parts of the course
* provide as many of the selected courses as possible
* the distance between back-to-back classes
* whether an overlap is allowed between two classes
* keep the existing schedule as much as possible
* substitute courses are only used if a selected course is not available
* a section choice that prevents the fewest future students from also getting the course

Once the assistant has suggested a schedule, a student can make changes to the schedule until she finds a combination of times for the classes that meets her needs.

Additional information is available in the [Student Scheduling Assistant Manual](scheduling-assistant).


### Wait-Listing

If a course and the student status allow for wait-listing, it can be wait-listed on the **Course Requests** table using the **Wait-List** checkbox. Suppose the course is not available for the student, e.g., because it is full. In that case, it can also be wait-listed on the **List of Classes** (using the **Wait-List** checkbox on the line with the course) or on the [Alternatives](../alternatives-for-class) dialog when the course/class is clicked (using the **Wait-List** button).

![Student Scheduling Assistant](../images/student-scheduling-assistant-6.png){:class='screenshot'}

Additional properties can be entered on the [Wait-List Preferences](../wait-list-preferences-for-a-course) dialog when the wait-listed course is clicked from the **List of Classes** table.

![Alternatives for Class](../images/wait-list-preferences-for-a-course.png){:class='screenshot'}

It is possible to wait-list for a course swap or a different section of the same course. In this case, the enrolled course that is to be replaced with the wait-listed course is selected on the [Wait-List Preferences](../wait-list-preferences-for-a-course) dialog. The original course is then also listed in the **Wait-Listed Courses** table (**Replaces** column).

If the wait-listed course has alternatives provided on the **Course Requests**, these courses are also being wait-listed if they allow for wait-listing. That is, if space becomes available for the student in the alternative course before there is space available in the first-choice course, UniTime will enroll the student in the alternative course instead. The alternative courses are also listed in the **Wait-Listed Courses** table and in the [Wait-List Preferences](../wait-list-preferences-for-a-course) dialog.


### Re-Scheduling

When re-scheduling is enabled, students can be automatically moved around the course when there is a course change. This happens when an instructional offering is being unlocked (the **Unlock** button is clicked on the [Instructional Offering Detail](../instructional-offering-detail) page, *reload-offering* action) or when the online scheduling server is being reloaded (*check-offering* action). Changes are only made to the course that is being updated (the rest of the student's schedule is left untouched), allowing students to be moved when

- a student is enrolled in a class that has been cancelled, *(e.g., a class has been cancelled)*
- a student has a time conflict that is not allowed, i.e., *(e.g., a class has been moved to a different time)*
  - they do not have an individual [reservation](../edit-reservation) or a reservation override that has the *Allow Time Conflict* checked,
  - the [scheduling subpart](../edit-scheduling-subpart) does not allow for *Student Overlaps*,
  - and there is no matching *Ignore Student Conflicts* distribution preference,
- a student has an incomplete or an invalid enrollment *(e.g., a course configuration has been changed and a new scheduling subpart added)*
  - a student needs one class of each scheduling subpart of one course configuration, following the parent-child relations when defined.

Students will **not be moved** when a class, configuration, reservation, or offering limit is decreased (when the enrollment gets over the limit), or when student scheduling is disabled for a class.

Students are processed in the order of the course priority (position of the course on the [Course Requests](../student-course-requests) table), each student with a problem (one of the three listed above) is either moved to some other enrollment (UniTime will try to keep as much of the existing registration or their original timetable as possible) or dropped from the course when no possible enrollment is available for the student. If wait-listing is enabled, the dropped student is wait-listed for the course with the wait-listing timestamp set to the original enrollment date (to retain the enrollment order).

If wait-listing is enabled, the students wait-listed for the course are processed just after the re-scheduling is done. So, for example, when a new class is added or a class limit is increased, the wait-listed students will get automatically enrolled if the new enrollment does not conflict with the rest of their schedule. However, students that do not have a problem, or are not being wait-listed, are kept where they are even if moving them would allow for some other student to get in.

### Scheduling Assistant Settings

A lot of the settings for the [Student Course Requests](#course-requests-settings) apply to the Scheduling Assistant page, too. 

In order for students to have access to the [Student Scheduling Assistant](../student-scheduling-assistant), the *Student* role needs to have *Student Scheduling Can Register* [permission](../permissions). The *Student Scheduling Can Require Preferences* permission is needed to be able to mark class and instructional method preferences as required.

If student statuses are being used (see Administration > Other > [Student Status Types](../student-scheduling-status-types)), the student's status must allow for **Assistant** for the page to be available and **Student Enroll** to make changes. The default student status is set on the Administration > Academic Sessions > [Academic Sessions](../academic-sessions) page; individual student statuses can be set on the [Online Student Scheduling Dashboard](online-student-scheduling-dashboard) or by advisors using the [Advisor Course Recommendations](../advisor-course-recommendations) page.

Courses of a particular [Course Type](../course-types) can be made unavailable for students to select on the [Student Scheduling Assistant](../student-scheduling-assistant) page, when the appropriate course type is not allowed on the [student scheduling status](../student-scheduling-status-types). Such a course does not show up in the [Course Finder](../course-finder) dialog. Courses controlled by a [department](../departments) that does not have **Student Scheduling** enabled will also not be available for the students to find and select. This can be further adjusted using the [Student Scheduling Rules](../student-scheduling-rules).

[Page access statistics and control](../access-statistics) is available for the [Student Scheduling Assistant](../student-scheduling-assistant) page. It can be configured using the following properties:
* `unitime.accessControl.sectioning.activeLimitInMinutes`
    * Number of minutes of inactivity for the user to get the Inactive Warning.
    * Defaults to 15 minutes.
* `unitime.accessControl.sectioning.maxActiveUsers`
    * Maximal number of users using the page at the same time (not set or zero for disabled).
    * Not set by default.

#### Notifications

Students can be automatically emailed about a change in their schedule using the various notifications. These are configured with the [student statuses](../student-scheduling-status-types), with the following **Notifications** options:

* **Student Request Change** Student made a change on the [Student Course Requests](student-course-requests) page
* **Student Enrollment Change** Student made a schedule change on the [Student Scheduling Assistant](student-scheduling-assistant) page
* **Admin Request Change** Admin or advisor made a change on the [Student Course Requests](student-course-requests) page
* **Admin Enrollment Change** Admin or advisor made a schedule change on the [Student Scheduling Assistant](student-scheduling-assistant) page
* **Enrollment Approval** Consent has been approved or denied
* **Course Schedule Change** A class that the student has enrolled in has been moved to a different time and/or room
* **Course Enrollment Change** There has been a change in the student schedule due to wait-listing or re-scheduling (e.g., student was moved from a cancelled class)
* **Course Failed Enrollment Change** An automatic enrollment change has failed (when an external enrollment provider is used)
* **External Enrollment Change** Student schedule has been changed externally (outside the UniTime user interface)

The student notifications can also be adjusted by setting `unitime.enrollment.email.` properties in the [Application Configuration](../application-configuration).

Instructors can also be notified about a schedule change of a class they are assigned to. These can be configured by the following [Application Configuration](../application-configuration) settings:

* Set `unitime.notifications.instructorChanges.enabled` to true to enable instructor notifications (defaults to false).
* Set `unitime.notifications.instructorChanges.checkNotificationDates` to true to automatically email instructors about their schedule changes only during the notification dates set on the [academic session](../academic-sessions).
* Set `unitime.notifications.instructorChanges.checkAssignment` to true to notify instructors about class assignment changes (class assigned/removed to/from an instructor).
* Set `unitime.notifications.instructorChanges.checkCancellations` to true to notify instructors about class cancellation changes (assigned class cancelled or reopened).
* Set `unitime.notifications.instructorChanges.includeLink` to true to include the link to UniTime in the instructor email notification ([Personal Schedule](../personal-schedule); UniTime URL needs to be configured using `unitime.url`)
* Set `unitime.notifications.instructorChanges.includeSchedule` to true to include the list of all currently assigned classes that the instructor has in the email notification.
* Set `unitime.notifications.instructorChanges.checkTime` to true to notify instructors about class time changes (class assigned to an instructor has a different time).
* Set `unitime.notifications.instructorChanges.checkRoom` to true to notify instructors about class room changes (class assigned to an instructor has a different room)
* Set `unitime.notifications.instructorChanges.checkShare` to true to notify instructors about check/display instructor's percent share, responsibility, and check for conflict changes (defaults to false).

#### Wait-Listing & Re-Scheduling

The wait-listing (or re-scheduling) of each course can be turned on or off on the [Edit Course Offering](../edit-course-offering) page for the controlling course, using the Wait-Listing dropdown. It has the following options:

* **Wait-Listing Enabled** Wait-listing is enabled for the instructional offering.
* **Re-Scheduling Enabled**: Wait-listing is not enabled; however, students can be automatically re-scheduled for the instructional offering.
* **Wait-Listing Disabled** Wait-listing and re-scheduling are not enabled for the instructional offering.

There are a few [Application Configuration](../application-configuration) parameters related to wait-listing and re-scheduling, namely:

* `unitime.offering.waitListDefault` default setting for the Wait-Listing of a course (defaults to Disabled, can also be set to Wait-Listing or Re-Scheduling)
* `unitime.enrollment.waitList.showWaitListPosition` allows students to see their position on the wait-list (defaults to true)
* `unitime.offering.waitListFilter` enable Wait-List filter on the [Instructional Offerings](../instructional-offerings) page (defaults to false)

Only students who have the **Wait-Listing** enabled in their [student status](../student-scheduling-status-types) can wait-list for a course, and only students who have the **Re-Scheduling** enabled in their [student status](../student-scheduling-status-types) may be automatically re-scheduled when there is a change in a course that allows for wait-listing or re-scheduling. The setup may also allow for wait-listing and/or re-scheduling to only happen during a certain time window, by setting the start/end dates on the status and with a fallback to a status that does not allow for wait-listing and/or re-scheduling.

By default, wait-listed students are ordered by:

- Course request priority (e.g., requests marked as [Vital by the advisor](#recommendation-settings) go first)
- Student request priority (Priority students first, then Senior, then Junior, then Sophomore, then Freshmen, then students not in a [priority group](#student-priority))
- First choice courses before alternatives (when a course with alternatives is wait-listed)
- Wait-listed timestamp (when the student wait-listed the course)

This can be changed by setting `unitime.custom.WaitListComparatorProvider` with a class implementing the [WaitListComparatorProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/WaitListComparatorProvider.java) class.
* **Tip:** Set it to [org.unitime.timetable.onlinesectioning.custom.purdue.TimeStampOnlyWaitListComparatorProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/purdue/TimeStampOnlyWaitListComparatorProvider.java) to only consider time stamps.

#### Scheduling Integrations

A number of custom interfaces can be implemented to allow for, for example:

* Integration with the Student Information System for student eligibility checking and enrollment changes ([StudentEnrollmentProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/StudentEnrollmentProvider.java))
* Integration with an approval workflow for various registration errors ([SpecialRegistrationProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/SpecialRegistrationProvider.java) and [WaitListValidationProvider](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/WaitListValidationProvider.java))
* The full list of customizations is available in the [Customizations](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/onlinesectioning/custom/Customization.java) enum.

For example, please see the Purdue-specific [Student Scheduling Assistant Manual](scheduling-assistant-purdue).

## Online Student Scheduling Dashboard

The Students > [Online Scheduling Dashboard](../online-student-scheduling-dashboard) can be used to monitor student registration & enrollments, change student status, etc. 

![Online Student Scheduling Dashboard](../images/online-student-scheduling-dashboard-4.png){:class='screenshot'}

The Online Student Scheduling Dashboard screen provides a tool for displaying a given set of course requests/student enrollments or students. The page also displays information from the sectioning log (either for a particular student or by a given filter). The page is available for administrators, scheduling deputies (can approve consent), student advisors (can change student enrollment), and course coordinators (can approve consent of the instructor). Course coordinators can only see courses that are assigned to them. The page has extensive filtering capabilities (by the student, group, curriculum, course, subject, consent, ...). It is possible to email students and/or change their scheduling status.

See [Student Scheduling Dashboard Manual](scheduling-dashboard) for additional documentation about the dashboard.

# Additional Documentation

There are also the following manuals:
* Student Course Requests Manual (Purdue specific [link](course-requests-purdue))
* [Student Scheduling Assistant Manual](scheduling-assistant) (Purdue specific [link](scheduling-assistant-purdue))
* [Student Scheduling Dashboard Manual](scheduling-dashboard) (Purdue specific [link](scheduling-dashboard-purdue))
