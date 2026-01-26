---
layout: default
title: XML Interfaces
---

Following XML interfaces reflect the UniTime data model. Data may be imported once (for each term) and/or periodically updated by a nightly batch process. It is also possible to maintain most of these data directly within UniTime, see Administration > Academic Sessions menu. Usually, records that have external ids (attribute externalId) are expected to be maintained in an external system, records without external ids are fully editable in UniTime.

Use [Data Exchange](data-exchange) page (menu Administration > Academic Sessions > Data Exchange) to import or export an XML. Alternatively, the [Data Exchange API](manuals/api#9data-exchange) can be used to import or export an XML.

### XML formats for import of academic session related data

* Academic session setup [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/sessionSetup.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/AcademicSessionSetup.dtd)]
    * Academic session, timetabling managers, departments, subject areas, solver groups, date patterns, time patterns, examination periods,
    academic areas, academic classifications, majors, minors, student groups, and accommodations.
    
* Other resources
    * Buildings and rooms [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/buildingRoomImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/BuildingRoom.dtd)]
        * Travel times [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/travelTimes.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/TravelTimes.dtd)]
        * Room Sharing [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/roomSharing.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/RoomSharing.dtd)]
    * Staff [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/sessionSetup.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Staff.dtd)]
    * Course catalog [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/courseCatalogImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/CourseCatalog.dtd)]
    * Event Load [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/eventLoad.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/EventLoad.dtd)] *-- One time load for Special Events and Course Related Events.*

**Academic session setup:** The XML import can be used to import/update the academic session, timetabling managers, departments, subject areas, solver groups, date patterns, time patterns, examination periods, academic areas, academic classifications, majors, minors, student groups, and/or student accommodations.
* Only sections that exist in the XML are imported.
* Set `incremental="true"` on the section for incremental update (inserting/updating only items listed in the file).
* Academic areas, classification, and majors are needed for curriculum timetabling and for curriculum reservations. Student groups are useful for group reservations.

**Buildings and rooms:** Please note that the [Buildings](buildings) and [Rooms](rooms) are not updated directly with the XML import, but the [Update Data](buildings#update-data) needs to be used to update the buildings and rooms.

**Staff:** Please note that this import does **NOT** update the [Instructors](instructors) directly. The imported records will show in the [People Lookup](people-lookup) dialog and can be pull into Instructors using the [Manage Instructor List](manage-instructor-list) page.

**Course catalog:** Please note that course catalog information does not get displayed directly in UniTime. The data can be used to create new courses during the [Roll Forward](roll-forward-session), Add New Course Offerings section.

The following APIs are still working, but are marked as **deprecated** (to be removed in future UniTime releases). If possible, please use the **Academic session setup** XML import instead.
* Student properties
    * Academic areas [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/academicAreaImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/AcademicArea.dtd)]
    * Academic classifications [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/academicClassificationImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/AcademicClassification.dtd)]
    * Majors [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/posMajorImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/PosMajor.dtd)]
    * Minors [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/posMinorImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/PosMinor.dtd)]
    * Student Groups [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/studentGroupImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/StudentGroup.dtd)] [DTD]
    * Student Accommodations [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/studentAccomodationImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/StudentAccomodation.dtd)] *(disabilities etc.)*
* Other resources
    * Departments [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/departmentImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Department.dtd)]
    * Subject areas [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/subjectAreaImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/SubjectArea.dtd)]

### XML formats for student data import and export

* Students [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/studentInfoImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Student.dtd)]
    * Student course requests [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/woebegonStudents.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/StudentSectioning.dtd)] *(pre-registration)*
    * Student class enrollments [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/studentEnrollmentImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/StudentEnrollment.dtd)]
* Curricula [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/curricula.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Curricula_3_2.dtd)]
* Last-like term student course demands [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/studentCrsDemandImport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/StudentCourse.dtd)] *(import only)*

[Course timetabling](course-timetabling) can be either based on curriculum information, last-like term student course demands, student course requests, or the actual student class enrollments. [Examination timetabling](examination-timetabling) requires student class enrollments. If both [course timetabling](course-timetabling) and [student scheduling](student-scheduling) is done in UniTime, at the very least, students need to be loaded from some external system.

**Students & Student course requests:** Use `incremental="true"` on the root element to enable incremental mode. In this mode, only the students present in the file are created or updated.

**Curricula:** Use `incremental="true"` on the root element to enable incremental mode. In this mode, only the curricula present in the file are created or updated.

### XML formats for course data and timetable import / export

* Course offerings [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/courseOfferingExport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/CourseOfferingExport.dtd)] *(including the course structure and time/room assignments)*
    * Including final/evening exams [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/courseOfferingWithExamsExport.xml)] *(including exam definitions and period/room assignments)*
    * Import example [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/courseOfferingWithExamsImport.xml)] *(including basis of the course structure, class and exam assignments)*
* Timetable [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/courseTimetableExport.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/CourseTimetable.dtd)] *(no course structure, only time/room assignments)*
    * Import example [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/courseTimetableImport.xml)]
* Reservations [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/reservations.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Reservations.dtd)]
* Preferences [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/preferences.xml)] [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Preferences.dtd)]

**Course offerings:** Use `incremental="true"` on the root element to enable incremental mode. In this mode, only the offerings present in the file are created or updated.

**Preferences:** Use `incremental="true"` on the root element to enable incremental mode. In this mode, only the departments, instructors, subparts, and/or classes present in the file have their preferences updated.

**Reservations:** Use `incremental="true"` on the root element to enable incremental mode. In this mode, only the offerings which do have reservations present in the file are updated (have their reservations reset to what is present in the XML file).

### XML formats for (online) data interchange

* Room availability [[Request XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/roomAvailabilityRequest.xml)]
    [[Response XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/roomAvailabilityResponse.xml)]
    [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/RoomAvailability.dtd)]
    *(see [Custom Room Availability](custom-room-availability))*

### Other XML formats:
* Permissions [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/permissions.xml)]
    [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Permissions.dtd)]
* Custom Reports [[Examples](https://github.com/UniTime/unitime/tree/master/Documentation/Reports)]
    [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/hqlReport.xml)]
    [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Reports.dtd)]
    *(see [HQL Reports](hql-reports) page)*
* Scripts
    [[Examples](https://github.com/UniTime/unitime/tree/master/Documentation/Scripts)]
    [[XML](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Examples/exampleScripts.xml)]
    [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/Script.dtd)]
    *(see [Scripts](scripts) page)*
* Point in time data [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/PointInTimeData.dtd)]
* Menu [[XML](https://github.com/UniTime/unitime/blob/master/JavaSource/menu-custom.xml)]
    [[DTD](https://github.com/UniTime/unitime/blob/master/Documentation/Interfaces/menu.dtd)]

**Permissions:** Use `incremental="true"` on the root element to enable incremental mode. In this mode, only listed roles will be created/updated.

**Menu:** Use this for custom menus.
* Unlike all the other XMLs, this file **cannot be imported** using the [Data Exchange](data-exchange) page!
* The custom menu XML file needs to be placed somewhere UniTime can read it and the `unitime.menu.custom` property needs to point to the file.

### Other APIs

Besides the above XML interfaces, there are additional RESTful interfaces. See [UniTime APIs](manuals/api) for more details. Also, the [Scripts](scripts) can be used to create additional custom imports and exports.