---
layout: manual
title: UniTime APIs
version: 4.4.91
updated: April, 2019
---

### Table of Contents
{:.no_toc}
* table
{:toc}


# Authentication


API calls can use HTTP-simple authentication with a user created using the UniTime’s [Users](../users-database-authentication) page, or if enabled (by setting the application property unitime.api.canUseToken to true) it can authenticated via an API token. The API token can be passed as an additional attribute (named `token`) on any API call. The user must have a default role with the appropriate API permission. The API token is available on the Users page (when enabled), it is computed using the username and hashed password (changing password will also change the API token for a user).





The available permissions are

* Api Retrieve Roles

* Api Retrieve Instructor Schedule

* Api Retrieve Class Info

* Api Retrieve Enrollments

* Api Retrieve Events (the appropriate event permissions are also needed)

* Api Retrieve Rooms (the appropriate room permissions are also needed)

* Api Room Picture Upload

* Api Room Edit (the appropriate room permissions are also needed)

* Api Online Student Scheduling

* Api Data Exchange Connector

* Api Json Connector (the appropriate permissions are also needed, depends on the request)

* Api Retrieve Instructors

* Api Retrieve Curricula

* Api Retrieve Student Groups

# Cache Mode


It is possible to change the hibernate cache mode for a particular API connector by setting the `unitime.api.X.cacheMode` application property (where `X` is the connector name). For example, setting `unitime.api.enrollments.cacheMode=REFRESH` will make the /api/enrollments connector to never read the hibernate cache, but it will keep it updated.





Possible values are:

| **Cache Mode** | **Meaning** |
| GET | The session may read items from the cache, but will not add items, except to invalidate items when updates occur. |
| IGNORE | The session will never interact with the cache, except to invalidate cache items when updates occur. |
| NORMAL | The session may read items from the cache, and add items to the cache (default). |
| PUT | The session will never read items from the cache, but will add items to the cache as it reads them from the database. |
| REFRESH | The session will never read items from the cache, but will add items to the cache as it reads them from the database. |











# 1 User Roles


The api/roles call returns a list of academic sessions and roles for a user.





**URL:** `GET api/roles?id=<extid>`





**Example:**
```
curl -uadmin:admin http://demo.unitime.org/UniTime/api/roles?id=101
```





Example Response:
```
[
  {
    "sessionId": 223206,
    "reference": "Fal2007woebegon",
    "selected": false,
    "year": "2007",
    "term": "Fal",
    "campus": "woebegon",
    "beginDate": "2007-08-20",
    "endDate": "2007-12-15",
    "classEndDate": "2007-12-08",
    "examBeginDate": "2007-12-10",
    "eventBeginDate": "2007-07-20",
    "eventEndDate": "2008-01-15",
    "status": {
      "refenrece": "finished",
      "label": "Session Finished",
      "classes": false,
      "exams": []
    },
    "roles": [
      "Instructor"
    ]
  },
  ...
]
```


The `sessionId` is UniTime's unique id of the academic session. All the session-dependent calls either use this `sessionId` (usually as sid=<sessionId>) or the academic session reference (`term=<reference>`). Campus (woebegon) can be omitted if there is only one academic session with matching year and term. The current academic session is indicated by `selected=true` (this is the academic session that would be automatically selected for the user, if any), for students and instructors it is the current academic session (for schedule managers it is the first future session however).





There can be more information provided on the status, so one can avoid academic sessions that are being timetabled (course schedule has not been published yet) or that are already finished. In general, a student or an instructor can only see a schedule of classes if `classes` attribute is true. Similarly, only examinations of the type listed under `exams` are available to students to see (midterm is evening exams).





When the call is made without any id, it lists all available academic sessions.





**URL:** `GET api/roles`





**Example:**
```
curl -uadmin:admin http://demo.unitime.org/UniTime/api/roles
```





Returns: all academic session, including their dates and status.





# 2 Instructor Schedule


The following call will return a list of classes (instructor), courses (coordinator), and exams (instructor) for an instructor. Unlike the events API, it does not show individual meetings (see below), but the results are much more compact.





**URL:** `GET api/instructor-schedule?term=<reference>&id=<extid>`





Example:
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/instructor-schedule?term=Fal2010&id=101"
```


Example Response:
```
{
  "externalId": "101",
  "session": {
    "sessionId": 231379,
    "reference": "Fal2010woebegon"
  },
  "instructors": [
    {
      "instructorId": 231389,
      "externalId": "101",
      "firstName": "GEORGE",
      "lastName": "NEWMAN",
      "position": {
        "reference": "ASSOC_PROF",
        "label": "Associate Professor"
      },
      "department": {
        "code": "0101",
        "name": "Student Instructional Planning"
      }
    }
  ],
  "classes": [
    {
      "lead": true,
      "percentShare": 100,
      "course": [
        {
          "courseId": 135755,
          "subjectArea": "BIOL",
          "courseNumber": "101",
          "courseTitle": "Introduction to Biology",
          "control": true
        }
      ],
      "classId": 231425,
      "subpart": "Pso",
      "sectionNumber": "3",
      "limit": 4,
      "meetings": [
        {
          "dayOfWeek": "Thursday",
          "startTime": "8:30",
          "endTime": "9:20",
          "datePattern": "Full Term",
          "firstDate": "2010-08-26",
          "lastDate": "2010-12-09",
          "building": "EDUC",
          "roomNumber": "101",
          "roomType": "Classrooms",
          "roomCapacity": 20
        }
      ]
    },
    ...
  ],
  "courses": [],
  "exams": [
    {
      "examId": 231681,
      "name": "BIOL 101 ",
      "type": "final",
      "size": 4,
      "length": 180,
      "owners": [
        {
          "type": "Class",
          "classId": 231395,
          "subjectArea": "BIOL",
          "courseNumber": "101",
          "courseTitle": "Introduction to Biology",
          "subpart": "Lec",
          "sectionNumber": "1"
        }
      ],
      "period": {
        "date": "2010-12-13",
        "startTime": "13:00",
        "endTime": "16:00"
      },
      "room": [
        {
          "building": "EDUC",
          "roomNumber": "102",
          "roomType": "Classrooms",
          "roomCapacity": 2
        },
        {
          "building": "EDUC",
          "roomNumber": "101",
          "roomType": "Classrooms",
          "roomCapacity": 20
        }
      ]
    },
    ...
  ]
}
```


Please note that a cross-listed class can have multiple courses.


When the assigned room is not a room but a non-university location (e.g., SITE, OFF CAMPUS, OFFICE, etc.), there is `location` = name attribute instead of `building` and `roomNumber`.
```
  "meetings": [
    {
      "dayOfWeek": "Monday",
      "startTime": "13:30",
      "endTime": "17:20",
      "datePattern": "Full Term",
      "firstDate": "2015-01-12",
      "lastDate": "2015-04-27",
      "location": "SITE",
      "roomType": "Non-University Locations",
      "roomCapacity": 9999
    }
  ]
```





# 3 Class Info


The following calls return information about a particular class.





**URL:** `api/class-info?classId=<classId>`





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/class-info?classId=231423"
```


Example Response:
```
{
  "course": [
    {
      "courseId": 135755,
      "subjectArea": "BIOL",
      "courseNumber": "101",
      "courseTitle": "Introduction to Biology",
      "control": true
    }
  ],
  "classId": 231423,
  "subpart": "Pso",
  "sectionNumber": "1",
  "limit": 4,
  "meetings": [
    {
      "dayOfWeek": "Wednesday",
      "startTime": "14:30",
      "endTime": "15:20",
      "datePattern": "Full Term",
      "firstDate": "2010-08-25",
      "lastDate": "2010-12-08",
      "building": "EDUC",
      "roomNumber": "101",
      "roomType": "Classrooms",
      "roomCapacity": 20
    }
  ],
  "instructors": [
    {
      "lead": true,
      "percentShare": 100,
      "instructorId": 231389,
      "externalId": "101",
      "firstName": "GEORGE",
      "lastName": "NEWMAN",
      "position": {
        "reference": "ASSOC_PROF",
        "label": "Associate Professor"
      },
      "department": {
        "code": "0101",
        "name": "Student Instructional Planning"
      }
    }
  ],
  "exams": [
    {
      "examId": 231672,
      "name": "BIOL 101",
      "type": "midterm",
      "size": 11,
      "length": 120,
      "owners": [
        {
          "type": "Course",
          "courseId": 135755,
          "subjectArea": "BIOL",
          "courseNumber": "101",
          "courseTitle": "Introduction to Biology"
        }
      ],
      "period": {
        "date": "2010-10-26",
        "startTime": "20:00",
        "endTime": "22:00"
      },
      "room": [
        {
          "building": "THTR",
          "roomNumber": "101",
          "roomType": "Special Use Rooms",
          "roomCapacity": 4
        },
        {
          "building": "EDUC",
          "roomNumber": "104",
          "roomType": "Classrooms",
          "roomCapacity": 1
        },
        {
          "building": "EDUC",
          "roomNumber": "101",
          "roomType": "Classrooms",
          "roomCapacity": 20
        }
      ],
      "instructors": [
        {
          "instructorId": 231389,
          "externalId": "101",
          "firstName": "GEORGE",
          "lastName": "NEWMAN",
          "position": {
            "reference": "ASSOC_PROF",
            "label": "Associate Professor"
          },
          "department": {
            "code": "0101",
            "name": "Student Instructional Planning"
          }
        }
      ]
    }
  ]
}
```

# 4 Enrollments


Following call will return enrollments of a class, a course, an examination, or an event.


**URL:** `api/enrollments?classId=<classId>`


**URL:** `api/enrollments?courseId=<courseId>`


**URL:** `api/enrollments?examId=<examId>`


**URL:** `api/enrollments?eventId=<eventId>`


**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/enrollments?classId=231423"
```

Example Response:
```
[
  {
    "studentId": 232546,
    "externalId": "1011",
    "firstName": "Kevin",
    "lastName": "Student",
    "area": [
      "A"
    ],
    "classification": [
      "02"
    ],
    "major": [
      "M1"
    ],
    "courseId": 135755,
    "subjectArea": "BIOL",
    "courseNumber": "101",
    "courseTitle": "Introduction to Biology",
    "classId": 231423,
    "subpart": "Pso",
    "sectionNumber": "1"
  },
  ...
]
```



# 5 Events


The events API that is capable of returning any data displayed on the [Events](../events), [Event Timetable](../event-timetable), or [Event Room Availability](../event-room-availability) pages. The following URL is based on a personal timetable, restricting output to class events for which the person is instructor (i.e., not student or coordinator).


**URL:** `api/evens?type=PERSON&e:type=Class&e:role=instructor&term=Fall2014&ext=<extid>`


**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/events?type=PERSON&e:type=Class&e:role=instructor&term=Fal2010&ext=101"
```

(all class events for an instructor with external id 101)


**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/events?type=ROOM&r:text=EDUC+101&term=Fal2010"
```


(all events in room EDUC 101)


In general, all chips of the [event filter](../events-event-filter) are prefixed with e: (e:text is the remaining text, if present) and all chips of the [room filter](../events-room-filter) are prefixed with r: (r:text is the remaining text, if present).





Example Response:
```
[
  {
    "eventId": 234534,
    "eventName": "PHYS 101 Lec 2",
    "eventType": "Class",
    "meetings": [
      {
        "location": {
          "resourceType": "ROOM",
          "resourceId": 8023,
          "resourceName": "EDUC 101",
          "size": 20,
          "roomType": "Classrooms",
          "breakTime": 0,
          "ignoreRoomCheck": false
        },
        "meetingId": 234561,
        "meetingDate": "2010-08-24T00:00:00Z",
        "startSlot": 162,
        "endSlot": 174,
        "startOffset": 0,
        "endOffset": -10,
        "dayOfWeek": 1,
        "dayOfYear": 236,
        "past": false,
        "canEdit": false,
        "canDelete": false,
        "canCancel": false,
        "canApprove": false,
        "canInquire": false,
        "approvalDate": "2010-09-22T00:00:00Z",
        "approvalStatus": "Approved",
        "startTime": 1282649400000,
        "stopTime": 1282652400000
      },
      {
        "location": {
          "resourceType": "ROOM",
          "resourceId": 8023,
          "resourceName": "EDUC 101",
          "size": 20,
          "roomType": "Classrooms",
          "breakTime": 0,
          "ignoreRoomCheck": false
        },
        "meetingId": 234559,
        "meetingDate": "2010-08-26T00:00:00Z",
        "startSlot": 162,
        "endSlot": 174,
        "startOffset": 0,
        "endOffset": -10,
        "dayOfWeek": 3,
        "dayOfYear": 238,
        "past": false,
        "canEdit": false,
        "canDelete": false,
        "canCancel": false,
        "canApprove": false,
        "canInquire": false,
        "approvalDate": "2010-09-22T00:00:00Z",
        "approvalStatus": "Approved",
        "startTime": 1282822200000,
        "stopTime": 1282825200000
      },
      ...
    ],
    "contact": {
      "firstName": "Abraham",
      "lastName": "Root",
      "formattedName": "Root, A",
      "email": "test-admin@unitime.org"
    },
    "courseNames": [
      "PHYS 101"
    ],
    "courseTitles": [
      "Physics"
    ],
    "instruction": "Lecture",
    "instructionType": 10,
    "maxCapacity": 3,
    "enrollment": 3,
    "reqAttendance": false,
    "sectionNumber": "2",
    "canView": true,
    "canEdit": false,
    "sequence": 0
  },
  ...
]
```


## Event Details





All available information about a particular event can be retrieved using the same API, but with a different parameter. The response contains one event with all its conflicts and all meetings of the event (including cancelled and rejected meetings).





**URL:** `api/evens?eventId=<id>`



**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/events?eventId=234534"
```



Example Response:
```
{
  "eventId": 31162368,
  "eventName": "My Test Course Event",
  "eventType": "Course",
  "eventEmail": "muller@unitime.org",
  "meetings": [
    {
      "location": {
        "resourceType": "ROOM",
        "resourceId": 8024,
        "resourceName": "EDUC 102",
        "size": 2,
        "roomType": "Classrooms",
        "breakTime": 0,
        "ignoreRoomCheck": false
      },
      "meetingId": 31227904,
      "meetingDate": "2010-09-14T00:00:00Z",
      "startSlot": 114,
      "endSlot": 126,
      "startOffset": 0,
      "endOffset": 0,
      "dayOfWeek": 1,
      "dayOfYear": 257,
      "past": true,
      "canEdit": true,
      "canDelete": false,
      "canCancel": true,
      "canApprove": false,
      "canInquire": true,
      "approvalDate": "2016-01-08T00:00:00Z",
      "approvalStatus": "Approved",
      "startTime": 1284449400000,
      "stopTime": 1284453000000,
      "conflicts": [
        {
          "eventId": 235654,
          "eventName": "COM 101 Lec 9",
          "eventType": "Class",
          "location": {
            "resourceType": "ROOM",
            "resourceId": 8024,
            "resourceName": "EDUC 102",
            "size": 2,
            "roomType": "Classrooms",
            "breakTime": 0,
            "ignoreRoomCheck": false
          },
          "meetingId": 235667,
          "meetingDate": "2010-09-14T00:00:00Z",
          "startSlot": 108,
          "endSlot": 126,
          "startOffset": 0,
          "endOffset": -15,
          "dayOfWeek": 0,
          "dayOfYear": 257,
          "past": false,
          "canEdit": false,
          "canDelete": false,
          "canCancel": false,
          "canApprove": false,
          "canInquire": false,
          "approvalDate": "2010-09-22T00:00:00Z",
          "approvalStatus": "Approved"
        }
      ]
    },
    ...
  ],
  "contact": {
    "firstName": "Joe",
    "middleName": "S",
    "lastName": "Doe",
    "title": "",
    "formattedName": "Doe, Joe S",
    "externalId": "100",
    "email": "muller@unitime.org",
    "phone": ""
  },
  "notes": [
    {
      "id": 31195136,
      "date": "2016-01-08T14:29:44Z",
      "user": "A Root",
      "type": "Create",
      "meetings": "M 09/14, 2010 9:30a - 10:30a EDUC 102"
    },
    {
      "id": 31588354,
      "date": "2016-01-08T15:12:28Z",
      "user": "A Root",
      "type": "Cancel",
      "meetings": "W 09/15, 2010 9:30a - 10:30a EDUC 103",
      "note": "Event Approved using API"
    },
    ...
  ],
  "maxCapacity": 2,
  "enrollment": 2,
  "reqAttendance": true,
  "canView": true,
  "canEdit": true,
  "relatedObjects": [
    {
      "uniqueId": 231391,
      "type": "Class",
      "courseNames": [
        "ALG 101",
        "ALG 102",
        "BIOL 20100"
      ],
      "courseTitles": [
        "Algebra I",
        "Algebra II",
        "Principles of Microbiology"
      ],
      "name": "ALG 101 Lec 1",
      "instruction": "Lecture (Hybrid)",
      "instructionType": 10,
      "instructors": [
        {
          "firstName": "JOE",
          "lastName": "DOE",
          "formattedName": "Doe, Joe",
          "externalId": "100"
        }
      ],
      "locations": [
        {
          "resourceType": "ROOM",
          "resourceId": 8019,
          "resourceName": "EDUC 103",
          "size": 2,
          "roomType": "Classrooms",
          "breakTime": 0,
          "ignoreRoomCheck": false
        }
      ],
      "date": "Full Term",
      "time": "MWF 9:30a - 10:20a",
      "sectionNumber": "1",
      "selection": [
        799,
        135753,
        231390,
        231391
      ],
      "detailPage": "classDetail.do?cid\u003d231391"
    }
  ],
  "conflicts": [
    {
      "eventId": 235654,
      "eventName": "COM 10100 Lec 9",
      "eventType": "Class",
      "meetings": [
        {
          "eventId": 235654,
          "eventName": "COM 101 Lec 9",
          "eventType": "Class",
          "location": {
            "resourceType": "ROOM",
            "resourceId": 8024,
            "resourceName": "EDUC 102",
            "size": 2,
            "roomType": "Classrooms",
            "breakTime": 0,
            "ignoreRoomCheck": false
          },
          "meetingId": 235667,
          "meetingDate": "2010-09-14T00:00:00Z",
          "startSlot": 108,
          "endSlot": 126,
          "startOffset": 0,
          "endOffset": -15,
          "dayOfWeek": 0,
          "dayOfYear": 257,
          "past": false,
          "canEdit": false,
          "canDelete": false,
          "canCancel": false,
          "canApprove": false,
          "canInquire": false,
          "approvalDate": "2010-09-22T00:00:00Z",
          "approvalStatus": "Approved"
        }
      ],
      "contact": {
        "firstName": "Abraham",
        "lastName": "Root",
        "formattedName": "Root, Abraham"
      },
      "courseNames": [
        "COM 10100",
        "COM 10100"
      ],
      "courseTitles": [
        "Communications I",
        "Communications I"
      ],
      "instruction": "Lecture",
      "instructionType": 10,
      "maxCapacity": 1,
      "enrollment": 1,
      "reqAttendance": false,
      "sectionNumber": "9",
      "canView": true,
      "canEdit": false,
      "sequence": 0
    }
  ],
  "sequence": 0
}
```


## Create / Update Event





An event can be created or updated using the POST request, with the event in JSON format in the payload.





**URL**: `POST api/events?term=<TERM>`


Optional parameters:


* **email:** whether email confirmation is to be sent (boolean, default to true)
* **message:** message describing the change (to be used as a note in the event note of the change)





The term parameter is only needed when creating a new event.





**Example:**
```
curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @new-event.json "http://demo.unitime.org/UniTime/api/events?term=Fall2010"
```





Example Payload (new event):
```
{
  "eventName": "My Test Event",
  "eventType": "Special",
  "eventEmail": "muller@unitime.org",
  "contact": {
    "externalId": "100"
  },
  "meetings": [
    {
      "location": {
        "resourceName": "EDUC 102"
      },
      "meetingDate": "2010-09-14T00:00:00Z",
      "startSlot": 114,
      "endSlot": 126
    }
  ]
}
```


Example Payload (update event):
```
{
  "eventId": 31162368,
  "eventName": "My Test Course Event",
  "eventType": "Course",
  "eventEmail": "muller@unitime.org",
  "reqAttendance": true,
  "contact": {
    "externalId": "100"
  },
  "meetings": [
    {
      "meetingId": 31227904
    },
    {
      "location": {
        "resourceName": "EDUC 103"
      },
      "meetingDate": "2010-09-15T00:00:00Z",
      "startSlot": 114,
      "endSlot": 126
    }
  ],
  "relatedObjects": [
    {
      "type": "Class",
      "uniqueId": 231391
    }
  ]
}
```

Notes:
* Start/end slots are expressed as 5 minute intervals since midnight.
* Related objects are only needed for course-related event (eventType is Course), when changing the relations.
* Rooms can be looked up by their name (resourceName).




## Delete Event


An event can be deleted using DELETE request


**URL**: `DELETE api/events?eventId=<ID>`


Where eventId is the unique id of the event.





Optional parameters:
* **email:** whether email confirmation is to be sent (boolean, default to true)

## Approve / Cancel / Reject / Inquire


Meetings of an event can be approved, cancelled, rejected, or inquired about using the POST request with the added parameter operation.


**URL**: `POST api/events?operation=APPROVE|CANCEL|REJECT|INQUIRE`


With the event message as payload. The message only needs to contain eventId and meetings.meetingId for all the meetings that are to be updated.


Optional parameters:
* **email:** whether email confirmation is to be sent (boolean, default to true)
* **message:** message describing the change (to be used as a note in the event note of the change)


**Example:**
```
curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @approve.json "http://demo.unitime.org/UniTime/api/events?operation=APPROVE"
```



Example Payload (approve event):
```
{
  "eventId": 31162368,
  "meetings": [
    {
      "meetingId": 31555584
    }
  ]
}
```


Besides of the Api Retrieve Events permission, the appropriate event permissions are also needed to be able to successfully execute the requested operation.


The response contains the updated event, including the newly created event notes and the lists of created, updated, and deleted meetings (if any).


Example Response:
```
{
  "event": {...}
  "messages": [
    {
      "level": "INFO",
      "message": "Confirmation email sent to Doe, Joe S."
    }
  ],
  "notes": [
    {
      "id": 31588354,
      "date": "2016-01-08T15:12:27Z",
      "user": "A Root",
      "type": "Cancel",
      "meetings": "W 09/15, 2010 9:30a - 10:30a EDUC 103",
      "note": "Event Approved using API"
    }
  ],
  "updatedMeetings": [
    {
      "location": {
        "resourceType": "ROOM",
        "resourceId": 8019,
        "resourceName": "EDUC 103",
        "size": 2,
        "roomType": "Classrooms",
        "breakTime": 0,
        "ignoreRoomCheck": false
      },
      "meetingId": 31555584,
      "meetingDate": "2010-09-15T02:00:00Z",
      "startSlot": 114,
      "endSlot": 126,
      "startOffset": 0,
      "endOffset": 0,
      "dayOfWeek": 2,
      "dayOfYear": 0,
      "past": false,
      "canEdit": false,
      "canDelete": false,
      "canCancel": false,
      "canApprove": false,
      "canInquire": false,
      "approvalDate": "2016-01-08T15:12:27Z",
      "approvalStatus": "Cancelled",
      "startTime": 1284535800000,
      "stopTime": 1284539400000
    }
  ]
}
```


# 6 Rooms


The rooms API that is capable of returning a list of rooms and their properties.



**URL:** `api/rooms?term=<TERM>&r:name=<NAME>`


**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/rooms?term=Fal2010&r:type=Classrooms&r:text=EDUC"
```


As for the events API, all chips of the [room filter](../events-room-filter) can be used and are prefixed with `r:` (`r:text` is the remaining text, if present).


Example Response:
```
[
  {
    "externalId": "",
    "building": {
      "id": 1782,
      "abbreviation": "EDUC",
      "name": "Education Hall",
      "x": 1.0,
      "y": 1.0
    },
    "roomType": {
      "id": 425,
      "label": "Classrooms",
      "room": true,
      "order": 0
    },
    "capacity": 20,
    "examCapacity": 2,
    "x": 1.0,
    "y": 1.0,
    "controlDepartment": {
      "code": "0100",
      "external": true,
      "event": true,
      "externalAbbv": "LLR",
      "externalLabel": "Large Lecture Room",
      "canEditRoomSharing": false,
      "id": 231382,
      "abbv": "Centr",
      "label": "Central Office",
      "color": "#f032f0",
      "title": "0100 - Central Office ( EXT: Large Lecture Room )"
    },
    "eventDepartment": {
      "code": "0100",
      "external": true,
      "event": true,
      "externalAbbv": "LLR",
      "externalLabel": "Large Lecture Room",
      "canEditRoomSharing": false,
      "id": 231382,
      "abbv": "Centr",
      "label": "Central Office",
      "color": "#f032f0",
      "title": "0100 - Central Office ( EXT: Large Lecture Room )"
    },
    "departments": [
      {
        "code": "0101",
        "external": false,
        "event": true,
        "canEditRoomSharing": false,
        "id": 231383,
        "abbv": "Instr",
        "label": "Student Instructional Planning",
        "color": "#32f0f0",
        "title": "0101 - Student Instructional Planning"
      },
      {
        "code": "0100",
        "external": true,
        "event": true,
        "externalAbbv": "LLR",
        "externalLabel": "Large Lecture Room",
        "canEditRoomSharing": false,
        "id": 231382,
        "abbv": "Centr",
        "label": "Central Office",
        "color": "#f032f0",
        "title": "0100 - Central Office ( EXT: Large Lecture Room )"
      }
    ],
    "groups": [
      {
        "id": 1245148,
        "abbv": "Classroom",
        "label": "Classroom"
      }
    ],
    "features": [
      {
        "id": 1245150,
        "abbv": "CompPr",
        "label": "Computer Projection",
      },
      {
        "id": 1245149,
        "abbv": "FixSeat",
        "label": "Fixed Seating",
      }
    ],
    "examTypes": [
      {
        "id": 1540050,
        "reference": "midterm",
        "label": "Midterm",
        "final": false
      },
      {
        "id": 1540049,
        "reference": "final",
        "label": "Final",
        "final": true
      }
    ],
    "ignoreTooFar": false,
    "ignoreRoomCheck": false,
    "availability": "LLR Mon 7:30a - 6:30p\nLLR TWThF 7:30a - 1:30p\nInstr Tue 1:30p - 3:30p\nLLR TWThF 3:30p - 6:30p\nLLR Wed 1:30p - 3:30p\nInstr Thu 1:30p - 3:30p\nLLR Fri 1:30p - 3:30p",
    "eventAvailability": "",
    "defaultEventStatus": 1,
    "defaultBreakTime": 0,
    "canShowDetail": true,
    "canSeeAvailability": true,
    "canSeePeriodPreferences": true,
    "canSeeEventAvailability": true,
    "canChange": true,
    "canChangeAvailability": true,
    "canChangeControll": false,
    "canChangeExternalId": false,
    "canChangeType": false,
    "canChangeCapacity": false,
    "canChangeExamStatus": false,
    "canChangeRoomProperties": false,
    "canChangeEventProperties": false,
    "canChangePicture": true,
    "canChangePreferences": true,
    "canChangeGroups": true,
    "canChangeFeatures": true,
    "canChangeEventAvailability": true,
    "canDelete": false,
    "miniMapUrl": "https://maps.google.com/maps/api/staticmap?center\u003d1.0,1.0\u0026zoom\u003d15\u0026size\u003d300x200\u0026maptype\u003droadmap\u0026sensor\u003dfalse\u0026markers\u003dcolor:blue|1.0,1.0",
    "mapUrl": "https://maps.google.com/maps/api/staticmap?center\u003d1.0,1.0\u0026zoom\u003d16\u0026size\u003d600x400\u0026maptype\u003droadmap\u0026sensor\u003dfalse\u0026markers\u003dcolor:blue|1.0,1.0",
    "pictures": [],
    "lastChange": "Last update was made by A. Root at 10/19/2015 03:17PM",
    "sessionId": 231379,
    "sessionName": "Fal 2010 (woebegon)",
    "uniqueId": 8023,
    "abbv": "",
    "name": "101",
    "params": {
      "overbook": "1",
      "permId": "1"
    }
  },
  ...
]
```

The `r:id` parameter can be used to retrieve a single room (of the given unique id).


**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/rooms?term=Fal2010&r:type=Classrooms&r:id=8023"
```


When `r:id` is used, room sharing, event availability and examination period preferences are also included in the response.

## Room Pictures


The rooms API can be also used to retrieve, upload, or delete room pictures. To retrieve a room picture, use the following URL.


**URL:** `api/rooms?pictureId=<uniqueId>`


The following URL can be used to upload a picture (using PUT). The image can be given as a payload.


**URL:** `PUT api/rooms?roomId=<ROOM ID>`


**URL:** `PUT api/rooms?term=<TERM>&room=<ROOM NAME>`



**Example:**
```
curl -uadmin:admin -k -X PUT --data-binary @picture.png -H "Content-Type:image/png" -H "Content-Disposition:attachment; filename=picture.png" "http://demo.unitime.org/UniTime/api/rooms?term=Fal2010&room=EDUC+101"
```


The content type can be defined by header parameter (Content-Type) or in URL (parameter `contentType`). File name can be defined by header parameter (Content-Disposition) or in URL (parameter `name`). Picture (attachment) type can be defined by type parameter (`reference` of the Attachment Type). Future academic sessions may be also updated by setting `future` parameter to 1. Returned message contains information about the created / updated picture.



Example Response:
```
{
  "uniqueId": 13369344,
  "name": "picture.png",
  "type": "image/png",
  "timeStamp": 1445972028704
}
```



The unique id can be used to retrieve a picture. The available pictures of a room are returned in the rooms message, in the `pictures` parameter (as list of the above responses).





A picture can be deleted using `DELETE` with the following URL:





**URL:** `DELETE api/rooms?pictureId=<PICTURE ID>`



**Example:**
```
curl -uadmin:admin -k -X DELETE "http://demo.unitime.org/UniTime/api/rooms?pictureId=13369344"
```


A picture is identified by its picture id. The returned message contains information about the deleted picture.


For upload and delete of room pictures, the Api Room Picture Upload permission is needed.

## Create / Update Room


The rooms API can be used to create or update a room (using POST). The payload message is the same (in the same format as the GET message, though a lot of information can be omitted). A new room is created when no room id is provided. A room is updated when a room id is provided (in the message or in the url, using either roomId parameter or a combination of term and room).





**URL:** `POST api/rooms?term=<TERM>`



**Example:**
```
curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @room.json "http://demo.unitime.org/UniTime/api/rooms?term=Fal2007&future=1"
```


Example POST Message:
```
{
  "building" : { "abbreviation" : "EDUC" },
  "name" : "101F",
  "roomType" : { "reference" : "genClassroom", "room" : true },
  "capacity" : 10,
  "controlDepartment":  { "code" : "0101" },
  "departments" : [
    { "code" : "0100" },
    { "code" : "0101", "preference" : { "code" : "P" } }
  ],
  "externalId" : "EDUC-101F-TWR",
  "area" : 100.0,
  "x" : 48.8583736,
  "y" : 2.2922926,
  "abbv" : "Eifell Tower",
  "eventDepartment" : { "code" : "0100" },
  "groups" : [
    { "abbv" : "Classroom" },
    { "abbv" : "Biol Labs" , "department" : { "code" : "0101" } }
  ],
  "features" : [
    { "abbv" : "AudRec" },
    { "abbv" : "Comp" }
  ],
  "examCapacity" : 5,
  "examTypes" : [
    { "reference" : "final" }
  ],
  "breakTime" : null,
  "eventStatus" : null,
  "eventNote" : "What the hack?",
  "roomSharingNote" : "Sorry, no sharing!"
}
```

For update, room id can be present in the message (`uniqueId` parameter), or given as a parameter in the URL (`roomId`). A room can be also looked up by providing term and room parameters (e.g., `term=Fal2010&room=EDUC+101`). It is possible to mark which parts are to be updated by using `flag` parameter, one or more of the following flags can be used:
`room_properties`, `exam_properties`, `event_properties`, `groups`, `features`





Future academic sessions may be also updated by setting `future` parameter to `1` or to `true`. The returned message contains the created / updated room.





Another `example: curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @room.json "http://demo.unitime.org/UniTime/api/rooms?term=Fal2007&room=EDUC+101F&future=1&flag=features"`





Only room features of the EDUC 101F will be updated, in Fall 2007 and all the future academic sessions (where a room with the matching permanent id exists).

## Delete Room


A room can be deleted using a DELETE action.





**URL:** `DELETE api/rooms?term=<TERM>&room=<NAME>`


**URL:** `DELETE api/rooms?roomId=<ROOM ID>`



Future academic sessions may be also updated by setting `future` parameter to `1` or to `true`.





For create, update and delete, the Api Room Edit permission is needed together with the appropriate room permissions (e.g., it is not possible to create a room without the AddRoom permission).





# 7 Buildings


The buildings API can be used to retrieve and/or update buildings for a particular academic session. It has the following properties:





#### To request a list of buildings for a particular term (permission ApiRetrieveRooms is needed)





**URL:** `api/buildings?term=<TERM>`





**Example:**
```
curl -uadmin:admin http://demo.unitime.org/UniTime/api/buildings?term=Fal2010
```


Example Response:
```
[
  {
    "id": 1782,
    "abbreviation": "EDUC",
    "name": "Education Hall",
    "x": 1.0,
    "y": 1.0,
    "externalId": "WEOBEGON-EDUC"
  },
  {
    "id": 1783,
    "abbreviation": "THTR",
    "name": "Theater of Performing Arts",
    "x": 2.0,
    "y": 1.0,
    "externalId": "WEOBEGON-THTR"
  }
]
```


#### To create or update an existing building


**URL:** `POST api/buildings?term=<TERM>`


With the payload containing a room that needs to be created (no id) or updated (has id).





**Example:**
```
curl -u admin:admin -X POST -H "Content-Type:application/json;charset=UTF-8" -d @building.json http://demo.unitime.org/UniTime/api/buildings?term=Fal2010
```





with the following content in the building.json:
```
{
  "abbreviation": "BRNG",
  "name": "Beering Hall",
  "x": 40.425582,
  "y": -86.9184694,
  "externalId": "TEST-BRNG"
}
```


A created or updated building is returned:
```
{
  "id": 36995072,
  "abbreviation": "BRNG",
  "name": "Beering Hall",
  "x": 40.425582,
  "y": -86.9184694,
  "externalId": "TEST-BRNG"
}
```



Permission ApiRoomEdit is needed together with BuildingAdd or BuildingEdit respectively.


#### To delete an existing building


**URL:** `DELETE UniTime/api/buildings?term=<TERM>&id=<ID>`


**URL:** `DELETE UniTime/api/buildings?term=<TERM>&externalId=<EXTID>`


**URL:** `DELETE UniTime/api/buildings?term=<TERM>&building=<ABBV>`


**Example:**
```
curl -u admin:admin -X DELETE http://demo.unitime.org/UniTime/api/buildings?term=Fal2010\&id=36995072
```


**Example:**
```
curl -u admin:admin -X DELETE http://demo.unitime.org/UniTime/api/buildings?term=Fal2010\&externalId=TEST-BRNG
```


**Example:**
```
curl -u admin:admin -X DELETE http://demo.unitime.org/UniTime/api/buildings?term=Fal2010\&building=BRNG
```


Permission ApiRoomEdit is needed together with BuildingDelete.

# 8 Online Student Scheduling


The API allows for pretty much all the calls of the [SectioningService](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/services/SectioningService.java) are covered, except of those related to HTTP session attributes (e.g., last request / schedule). The [SectioningService](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/services/SectioningService.java) is for instance used by the [Student Scheduling Assistant](../student-scheduling-assistant) and the [Online Student Scheduling Dashboard](../online-student-scheduling-dashboard) pages.


The Api Online Student Scheduling permission is needed to use this API.

### List matching course offerings


**URL:** `GET api/sectioning?operation=listCourseOfferings&term=<TERM>&query=<QUERY>&limit=<LIMIT>`


**Example:**
```
curl -u admin:admin "http://demo.unitime.org/UniTime/api/sectioning?term=Fal2010&operation=listCourseOfferings&query=AL"
```


### Retrieve course details


**URL:** `GET api/sectioning?operation=retrieveCourseDetails&term=<TERM>&course=<COURSE>`


**Example:**
```
curl -u admin:admin "http://demo.unitime.org/UniTime/api/sectioning?term=Fal2010&operation=retrieveCourseDetails&course=ALG+101"
```

### List classes for a course


**URL:** `GET api/sectioning?operation=listClasses&term=<TERM>&course=<COURSE>`


**Example:**
```
curl -u admin:admin "http://demo.unitime.org/UniTime/api/sectioning?term=Fal2010&operation=listClasses&course=ALG+101"
```

### Save course requests (when in the Registration mode)


**URL:** `POST api/sectioning?operation=saveRequest&term=<TERM>&studentId=<EXT ID>`


**Example:**
```
curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @courses.json "http://demo.unitime.org/UniTime/api/sectioning?term=Fal2010&studentId=1001&operation=saveRequest"
```


Example payload message:
```
{
  "alternatives": [],
  "courses": [
      {
          "requestedCourse": [
              {
                  "courseName": "ALG 101"
              }
          ],
          "waitList": false
      },
      {
          "requestedCourse": [
              {
                  "courseName": "COM 101"
              }
          ],
          "waitList": false
      },
      {
          "requestedCourse": [
              {
                  "courseName": "PSY 101"
              }
          ],
          "waitList": false
      },
      {
          "requestedCourse": [
              {
                  "courseName": "ECON 101"
              },
              {
                  "courseName": "ENGR 101"
              }
          ],
          "waitList": false
      },
      {
          "requestedCourse": [
              {
                  "courseName": "SOC 101"
              }
          ],
          "waitList": false
      },
      {
          "requestedCourse": [
              {
                  "freeTime": [
                      {
                          "days": [
                              0,
                              2,
                              4
                          ],
                          "length": 12,
                          "start": 90
                      }
                  ]
              }
          ],
          "waitList": false
      }
  ]
}
```

### Compute a schedule


**URL:** `POST api/sectioning?operation=section&term=<TERM>&studentId=<EXT ID>`

**Example:**
```
curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @section.json "http://demo.unitime.org/UniTime/api/sectioning?term=Fal2010&studentId=1001&operation=section"
```



Example Request Message:
```
{
    "request": {
        "alternatives": [],
        "courses": [
            {
                "requestedCourse": [
                    {
                        "courseName": "ALG 101"
                    }
                ],
                "waitList": false
            },
            {
                "requestedCourse": [
                    {
                        "courseName": "COM 101"
                    }
                ],
                "waitList": false
            },
            {
                "requestedCourse": [
                    {
                        "courseName": "PSY 101"
                    }
                ],
                "waitList": false
            },
            {
                "requestedCourse": [
                    {
                        "courseName": "ECON 101"
                    },
                    {
                        "courseName": "ENGR 101"
                    }
                ],
                "waitList": false
            },
            {
                "requestedCourse": [
                    {
                        "courseName": "SOC 101"
                    }
                ],
                "waitList": false
            },
            {
                "requestedCourse": [
                    {
                        "freeTime": [
                            {
                                "days": [
                                    0,
                                    2,
                                    4
                                ],
                                "length": 12,
                                "start": 90
                            }
                        ]
                    }
                ],
                "waitList": false
            }
        ]
    }
}
```

Example Response:
```
{
  "assignments": [
    {
      "courseId": 135753,
      "assigned": true,
      "subject": "ALG",
      "courseNbr": "101",
      "title": "Algebra I",
      "hasUniqueName": true,
      "notAvailable": false,
      "locked": false,
      "waitListed": false,
      "assignments": [
        {
          "courseAssigned": true,
          "courseId": 135753,
          "classId": 231391,
          "subpartId": 231390,
          "days": [
            0,
            2,
            4
          ],
          "start": 114,
          "length": 12,
          "breakTime": 10,
          "instructos": [
            "J Doe"
          ],
          "instructoEmails": [
            ""
          ],
          "rooms": [
            "EDUC 103"
          ],
          "alternative": false,
          "hasAlternatives": false,
          "distanceConflict": false,
          "datePattern": "08/23 - 12/10",
          "subject": "ALG",
          "courseNbr": "101",
          "subpart": "Lec",
          "section": "1",
          "number": "1",
          "title": "Algebra I",
          "limit": [
            2,
            2
          ],
          "pin": false,
          "backToBackDistance": 0,
          "saved": true,
          "dummy": false,
          "cancelled": false,
          "credit": "3|3 Semester Hours of Collegiate Credit"
        }
      ]
    },
    ...
  ],
  "canEnroll": true,
  "value": 0.9991
}
```

### Compute suggestions


**URL:** `POST api/sectioning?operation=computeSuggestions&term=<TERM>&studentId=<EXT ID>`


**Example:**
```
curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @suggestions.json "http://demo.unitime.org/UniTime/api/sectioning?term=Fal2010&studentId=1001&operation=computeSuggestions"
```



Example Request Message:
```
{
  "request": {
    "courses": [
      {
        "requestedCourse": [{ "courseName": "ALG 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "COM 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "PSY 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "ECON 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "SOC 101"}],
        "waitList": false
      }
    ],
    "alternatives": []
  },
  "currentAssignment": [
        {
          "courseId": 135761,
          "classId": 231489,
          "pin": false,
          "saved": false
        },
        {
          "courseId": 135762,
          "classId": 231496,
          "pin": false,
          "saved": false
        },
        {
          "courseId": 135774,
          "classId": 231570,
          "pin": false,
          "saved": false
        }
      ]
    }
  ],
  "selectedAssignment": 0
}
```

### Enroll


**URL:** `api/sectioning?operation=enroll&term=<TERM>&studentId=<EXT ID>`


**Example:**
```
curl -u admin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @enroll.json "http://demo.unitime.org/UniTime/api/sectioning?term=Fal2010&studentId=1001&operation=enroll"
```


Example Request Message:
```
{
  "request": {
    "courses": [
      {
        "requestedCourse": [{ "courseName": "ALG 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "COM 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "PSY 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "ECON 101"}],
        "waitList": false
      },
      {
        "requestedCourse": [{ "courseName": "SOC 101"}],
        "waitList": false
      }
    ],
    "alternatives": []
  },
  "currentAssignment": [
        {
          "courseId": 135761,
          "classId": 231489
        },
        {
          "courseId": 135762,
          "classId": 231496
        },
        {
          "courseId": 135774,
          "classId": 231570
        }
      ]
    }
  ]
}
```

The above list of operation is not exhaustive. For the full list of available operations, see the [OnlineStudentSchedulingConnector.Operation](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/api/connectors/OnlineStudentSchedulingConnector.java#L147) enum.


# 9 Data Exchange


The api/exchange connector has the same capability as the [Data Exchange](../data-exchange) page. This means that it can be used to export or to import any XML file that are listed on the [XML Interfaces](https://www.unitime.org/uct_interfaces.php) web page. Permission Api Data Exchange Connector is required.



To export an XML file, use the following URL. The `type` is the name of the root element of the XML you want to export.





**URL:** `GET api/exchange?term=<TERM>&type=<TYPE>`



**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/exchange?term=Fal2010&type=studentEnrollments" >enrollments.xml
```



To import an XML file, use the following URL. All the necessary information (XML type, academic session, etc.) is taken from the POSTed XML file.



**URL:** `POST api/exchange`


**Example:**
```
curl -uadmin:admin -k -X POST -H "Content-Type:application/xml;charset=UTF-8" -d @enrollments.xml http://demo.unitime.org/UniTime/api/exchange
```



Example Response:
```
<?xml version="1.0" encoding="UTF-8"?>
<html>
  <p>&lt;font color='gray'&gt;&amp;nbsp;&amp;nbsp;--Transaction started.&lt;/font&gt;</p>
  <p>Loading classes...</p>
  <p>Loading students...</p>
  <p>Importing enrollments...</p>
  <p>0 students changed</p>
  <p>&lt;font color='gray'&gt;&amp;nbsp;&amp;nbsp;--Transaction committed.&lt;/font&gt;</p>
</html>
```


The response contains the same log as is visible on the [Data Exchange](../data-exchange) during the import, in an HTML format.




# 10 JSON RPC


All the calls from the GWT code (e.g., event management) that are using the GWT RPC Command pattern (the request implements the [GwtRpcRequest](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/command/client/GwtRpcRequest.java) class, the response implements the [GwtRpcResponse](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/command/client/GwtRpcResponse.java) class and the server call is implemented by a Spring service annotated with the [@GwtRpcImplements](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/command/server/GwtRpcImplements.java) annotation) can be called using the api/json connector. The permission Api Json Connector is required together with the appropriate permissions that are checked by the appropriate implementation.





**URL**: `POST api/json?type=<REQUEST CLASS>`


The `type` contains the full class name of the request class and the payload is a JSON representation of the request content (an instance of the request class). The response contains the response class in the JSON format.


The following example is using the [EventEnrollmentsRpcRequest](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/shared/EventInterface.java) class to retrieve the list of student enrollments of a particular event. The response is a list of enrollments in the [ClassAssignmentInterface.Enrollment](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/gwt/shared/ClassAssignmentInterface.java#L1198) format.





**Example:**
```
curl -uadmin:admin -k -X POST -H "Content-Type:application/json;charset=UTF-8" -d @event-enrollments.json "http://demo.unitime.org/UniTime/api/json?type=org.unitime.timetable.gwt.shared.EventInterface%24EventEnrollmentsRpcRequest"
```


Example Request:
```
{ eventId: 236212, sessionId: 231379 }
```

Example Response:
```
[
  {
    "student": {
      "id": 231849,
      "externalId": "1001",
      "name": "Student, Andrew",
      "area": [
        "A"
      ],
      "classification": [
        "02"
      ],
      "major": [
        "M3"
      ],
      "canShowExternalId": false,
      "canUseAssitant": true,
      "canRegister": false
    },
    "course": {
      "courseId": 135753,
      "assigned": true,
      "subject": "ALG",
      "courseNbr": "101",
      "hasUniqueName": true,
      "notAvailable": false,
      "locked": false,
      "waitListed": false,
      "assignments": [
        {
          "courseAssigned": true,
          "courseId": 135753,
          "classId": 231391,
          "days": [],
          "start": 0,
          "length": 0,
          "breakTime": 0,
          "instructos": [],
          "instructoEmails": [],
          "rooms": [],
          "alternative": false,
          "hasAlternatives": true,
          "distanceConflict": false,
          "subject": "ALG",
          "courseNbr": "101",
          "subpart": "Lec  ",
          "section": "1",
          "number": "1",
          "pin": false,
          "backToBackDistance": 0,
          "saved": false,
          "dummy": false,
          "cancelled": false
        }
      ]
    },
    "priority": 1,
    "requestedDate": "2010-09-22T16:25:20Z",
    "enrolledDate": "2010-09-22T16:34:08Z"
  },
  ...
]
```




# 11 Instructors


The api/instructors call returns a list of instructors for the given department or academic session.





**URL:** `GET UniTime/api/instructors?id=<DEP_ID>`


**URL:** `GET UniTime/api/instructors?term=<TERM>&code=<DEPT_CODE>`


**URL:** `GET UniTime/api/instructors?term=<TERM>`





Where `DEP_ID` is the department unique id, `TERM` is the academic session reference, and `DEPT_CODE` is the department code.





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/instructors?term=Fal2010&code=0101"
```



Example Response:
```
[
  {
    "departmentId": 231383,
    "externalId": "Woebegon Dept 0101",
    "deptCode": "0101",
    "abbreviation": "Instr",
    "name": "Student Instructional Planning",
    "externallyManaged": false,
    "instructors": [
      {
        "instructorId": 231389,
        "externalId": "101",
        "firstName": "GEORGE",
        "lastName": "NEWMAN",
        "position": {
          "reference": "ASSOC_PROF",
          "label": "Associate Professor"
        }
      },
      {
        "instructorId": 231388,
        "externalId": "100",
        "firstName": "JOE",
        "lastName": "DOE",
        "position": {
          "reference": "CONT_LEC",
          "label": "Continuing Lecturer"
        }
      }
    ]
  }
]
```


# 12 Student Groups


The api/student-groups call returns a list of student groups for the given academic session.



**URL:** `GET UniTime/api/student-groups?term=<TERM>`





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/student-groups?term=Fal2010"
```





Example Response:
```
[{
    "id": 2195456,
    "abbreviation": "G1",
    "name": "Group 1",
    "students": [
      {
        "studentId": 231849,
        "externalId": "1001",
        "firstName": "Andrew",
        "lastName": "Student",
        "curriculum": [
          {
            "area": "A",
            "classification": "02",
            "major": "M3"
          }
        ]
      },
      {
        "studentId": 232460,
        "externalId": "1004",
        "firstName": "David",
        "lastName": "Student",
        "curriculum": [
          {
            "area": "A",
            "classification": "01",
            "major": "M1"
          }
        ]
      }
    ]
  },
  {
    "id": 2195457,
    "abbreviation": "G2",
    "name": "Group 2",
    "students": []
  }
]
```

# 13 Curricula


The api/curricula call returns a list of curricula for the given academic session.





**URL:** `GET UniTime/api/curricula?term=<TERM>`





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/curricula?term=Fal2010"
```



Example Response:
```
[
  {
    "id": 238654,
    "abbv": "A/M1",
    "name": "The Woebegon\u0027s Only Academic Area / Major 1",
    "editable": false,
    "multipleMajors": false,
    "academicArea": {
      "areaId": 142,
      "areaAbbv": "A",
      "areaName": "The Woebegon\u0027s Only Academic Area"
    },
    "majors": [
      {
        "majorId": 1201,
        "majorCode": "M1",
        "majorName": "Major 1"
      }
    ],
    "dept": {
      "deptId": 231383,
      "deptCode": "0101",
      "deptAbbv": "Instr",
      "deptName": "Student Instructional Planning"
    }
  },
  ...
]
```

The same filter parameters as on the Curricula page can be used to filter the results (with `c:` prefix), examples:


GET `UniTime/api/curricula?term<TERM>&c:department=0101&c:area=A`

GET `UniTime/api/curricula?term<TERM>&c:text=A/M1+or+A/M2`


To retrieve more details about a particular curriculum, use:


GET `UniTime/api/curricula?id=<CURR_ID>` (details about a particular curriculum)


GET `UniTime/api/curricula?term<TERM>&c:text=A/M1+or+A/M2&details=1` (return more information for all matching curricula)





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/curricula?term=Fal2010&c:text=A/M1&details=1"
```




Example Response:
```
[{
    "id": 238654,
    "abbv": "A/M1",
    "name": "The Woebegon\u0027s Only Academic Area / Major 1",
    "editable": true,
    "multipleMajors": false,
    "academicArea": {
      "areaId": 142,
      "areaAbbv": "A",
      "areaName": "The Woebegon\u0027s Only Academic Area"
    },
    "majors": [
      {
        "majorId": 1201,
        "majorCode": "M1",
        "majorName": "Major 1"
      }
    ],
    "dept": {
      "deptId": 231383,
      "deptCode": "0101",
      "deptAbbv": "Instr",
      "deptName": "Student Instructional Planning"
    },
    "clasf": [
      {
        "curriculumId": 238654,
        "clasfId": 238655,
        "name": "01",
        "nrStudents": 5,
        "enrollment": 5,
        "lastLike": 5,
        "projection": 5,
        "requested": 5,
        "clasf": {
          "clasfId": 61,
          "clasfCode": "01",
          "clasfName": "Junior Year"
        }
      },
      {
        "curriculumId": 238654,
        "clasfId": 238665,
        "name": "02",
        "nrStudents": 4,
        "enrollment": 4,
        "lastLike": 4,
        "projection": 4,
        "requested": 4,
        "clasf": {
          "clasfId": 62,
          "clasfCode": "02",
          "clasfName": "Senior Year"
        }
      }
    ],
    "courses": [
      {
        "courseId": 135754,
        "courseName": "BAND 101",
        "curriculumCourses": [
          {
            "id": 238670,
            "courseId": 135754,
            "clasfId": 238665,
            "courseName": "BAND 101",
            "share": 0.25,
            "enrollment": 1,
            "requested": 1
          }
        ]
      },
      {
        "courseId": 135755,
        "courseName": "BIOL 101",
        "curriculumCourses": [
          {
            "id": 238659,
            "courseId": 135755,
            "clasfId": 238655,
            "courseName": "BIOL 101",
            "share": 1.0,
            "enrollment": 5,
            "requested": 5
          },
          {
            "id": 238681,
            "courseId": 135755,
            "clasfId": 238665,
            "courseName": "BIOL 101",
            "share": 0.5,
            "enrollment": 2,
            "requested": 2
          }
        ]
      },
      ...
    ]
  }
]
```

# 14 Script


The api/script can be used to execute a script, check its progress, and retrieve the results.





To start a script use





**URL:** `POST UniTime/api/script?term=<TERM>&script=<SCRIPT>&queue=<true|false>&...`





If there is an input file, it can be passed as the message payload. Otherwise, the payload is empty (or GET can be used instead).





The `<SCRIPT>` is the name of the script. Additional script parameters can be included in the query.





When `queue=false`, the script will be executed immediately and the resulting file will be returned. When there is no resulting file, the script log will be returned instead.





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/script?term=Fal2010&script=Example+script&queue=false&dept=0100&subjects=ALG&subjects=BAND&subjects=BIOL&name=Johnny"
```



Starting the example script from [http://help.unitime.org/Scripts](../scripts)


Example Response (`queue=false`):
```
This is a test.
Žlutoucký kun úpel dábelské ódy.
```
***(contents of the resultant text file)***

When `queue=true`, the script is executed through the execution queue (the execution becomes visible on the Scripts page).


Example Response (`queue=true`):
```
{
  "id": "133c3bab-a9ac-477e-b49d-04af10ba238d",
  "name": "Example script",
  "status": "Waiting...",
  "progress": "",
  "owner": "Root, Abraham",
  "session": "Fal 2010 (woebegon)",
  "log": "",
  "host": "demo-173",
  "created": "2019-04-24T16:11:36Z",
  "canDelete": true,
  "executionRequest": {
    "id": 1736704,
    "name": "Example script",
    "parameters": {
      "subjects": "799,800,801",
      "name": "Johnny",
      "dept": "231382"
    }
  }
}
```

The execution id can be used to get additional information about the script.

## Execution Status





**URL:** `GET UniTime/api/script?id=<ID>`



**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/script?id=133c3bab-a9ac-477e-b49d-04af10ba238d"
```


Example Response:
```
{
  "id": "133c3bab-a9ac-477e-b49d-04af10ba238d",
  "name": "Example script",
  "status": "All done.",
  "progress": "",
  "owner": "Root, Abraham",
  "session": "Fal 2010 (woebegon)",
  "output": "test.txt",
  "log": "\u003cb\u003eStarting up…",
  "host": "demo-173",
  "outputLink": "qpfile?q\u003dJ4jV7c_EkI2SdFEkS4oOq-_AsnCAdQkHgtcTUJm-GCbCruzT1zTYIX9wBwi2zgNn",
  "created": "2019-04-24T16:11:36Z",
  "started": "2019-04-24T16:11:36Z",
  "finished": "2019-04-24T16:12:13Z",
  "canDelete": true,
  "executionRequest": {
    "id": 1736704,
    "name": "Example script",
    "parameters": {
      "subjects": "799,800,801",
      "name": "Johnny",
      "dept": "231382"
    }
  }
}
```


## Finished?





**URL:** `GET UniTime/api/script?finished=<ID>`





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/script?finished=133c3bab-a9ac-477e-b49d-04af10ba238d"
```





Returning true when the script has already finished, false otherwise.

## Script Log





**URL:** `GET UniTime/api/script?log=<ID>`





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/script?log=133c3bab-a9ac-477e-b49d-04af10ba238d"
```




## Resultant File





**URL:** `GET UniTime/api/script?output=<ID>`





**Example:**
```
curl -uadmin:admin "http://demo.unitime.org/UniTime/api/script?output=133c3bab-a9ac-477e-b49d-04af10ba238d"
```
