---
layout: default
title: Default Academic Session
---


There is no default to be set as different users can access different academic sessions. The following rules are applied in computation of the default session of a user. Only academic sessions that the user can access are considered. And if the user is a timetabling manager, only academic sessions for which he/she has a manager role are considered first. Similarly, if a No Role role is allowed, the sessions for which the user does not have any other role are only considered if there is no default among all sessions for which the user has a role.

**Rules**

* test and inactive academic sessions are ignored

* if there are two academic session with different initiative (campus) → there is no default

* based on the role either the current session, the first future session, or the first examination session is returned

* if there is no current or first future / examination session to return, the last active session is returned

**Details**

* **test session**: academic session status does have the test session toggle checked

* **inactive session**: academic session status does not have any edit / timetable / or no-role reporting enabled (e.g., sessions in the Initial Data Load and Session Finished states)

* **if there is no default session**: the user is redirected to Select Academic Session page after the login

* **current session**: current date is between event start and end dates

* **first future session**: among academic sessions that are after the current session (or that start after today if there is no current session), the first one is selected -- sessions are ordered by their session begin dates

* **first examination session**: it is the current session when it is still doing examination timetabling (final examination schedule is not published), first future session otherwise

**Permissions**

* first future session is returned to the users with primary role that has **Session Default First Future** permission (typically department schedule managers)

* first examination session is returned to the users with primary role that has **Session Default First Examination** (typically examination managers)

* the current session is returned to the users with primary role that has **Session Default Current** permission (usually all other roles)

**Otherwise** (e.g., there is no role, no such permission assigned, or no appropriate role based on the permission to return), the following session is returned:

1. current session
2. first future session (if there is no current session)
3. last active session (if there is no current or future session)
4. last session that is not a test session (including inactive sessions, i.e., if all available sessions are inactive)

Also, if the application property tmtbl.keeplastused.session is set to true (it defaults to false), the academic session that the user used last time is remembered and automatically returned as the default one (if it is among the sessions that are available to the user).
