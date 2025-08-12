---
layout: default
title: Manager Settings
---


## Screen Description

The Manager Settings screen provides a list of manager's settings, which can easily be changed by clicking on any of them.

![Manager Settings](images/manager-settings-1.png){:class='screenshot'}

Manager Settings help the users display information and select functionality that is most helpful for them in the input data section of the application.

## Details

The following settings are available

* **Automatically calculate number of classes and room size when editing configuration**
	* Yes (default) - Automatically calculate the number of classes in a scheduling subpart after the limit per class is entered in the [Instructional Offering Configuration](instructional-offering-configuration) screen
	* No - Do not calculate

* **Display last changes**
	* Yes (default) - in each non-editable screen, list who and when made the last change to the information displayed in the screen
	* No - do not display this section

* **Inherit instructor preferences on a class**
	* Ask - Ask about inheritance when an instructor is added in the [Edit Class](edit-class) screen
	* Always - Always apply instructor's preferences
	* Never (default) - Never apply instructor preferences

* **Display confirmation dialogs**
	* Yes (default) - Display pop-up windows with confirmation messages
	* No - Do not display these pop-ups

* **Sort classes on detail pages**
	* Yes - When "Sort By" is changed in the [Instructional Offerings](instructional-offerings) or [Classes](classes) screen, apply this sorting to the detail screens (such as [Instructional Offering Detail](instructional-offering-detail) or [Scheduling Subpart Detail](scheduling-subpart-detail)
	* No (default) - Keep sorting classes in the detail screens by name

* **Instructor name display format**
	* Last-first (Doe, Joe)
	* First-last (Joe Doe)
	* Initial-last (J M Doe)
	* Last-initial (default; Doe, J M)
	* First-middle-last (Joe Mark Doe)
	* Short (J M Doe)
	* Other options are available when registered on the [Default Manager Settings](default-manager-settings) page, see the [NameFormat](https://github.com/UniTime/unitime/blob/master/JavaSource/org/unitime/timetable/util/NameFormat.java) enum for the available options

* **Display room features in one column**
	* Yes (default) - All room features are listed in the Features column in the [Rooms](rooms) screen
	* No - Each feature has its column and for each room, a check is present in the appropriate column if the room has the feature

* **Show the option to set variable class limits**
	* Yes - The option is present in the [Instructional Offering Configuration](instructional-offering-configuration) and in the [Multiple Class Setup](multiple-class-setup) screen
	* No (default) - The option is turned off for the manager

* **Time grid display format**
	* Horizontal - Days on the left, times on top
	* Vertical (default) - Days on top, times on the left
	* Text - In the overview screens ([Instructional Offerings](instructional-offerings), [Classes](classes),...), the time preferences are spelled out as text

* **Time grid default selection**
	* Workdays x Daytime (default)
	* All Week x Daytime
	* Workdays x Evening
	* All Week x Evening
	* All Week x All Times

* **Display an icon or shortened text when ...**
	* In the table, show an **icon**, a **shortened text**, or the **full text** of the note

* **Menu style**
	* Dynamic On Top – Horizontal menu on the top of the page that moves with the window as the page is scrolled down.
	* Static On Top - Same menu as Dynamic On Top, but it is included in the page (it does not scroll with the page).
	* Tree On Side - Tree menu on the left side of the page, the closest to the menu in UniTime 3.1. It is fully collapsable and scrolls down with the page.
	* Stack On Side - Similar to the tree menu, but only one top section of the menu (Courses, Students, Examinations, ...) can be opened at a time. It is fully collapsable and scrolls down with the page.

## Operations

Click the column header to sort the table by that column. The second click on the same header will reverse the order.

### Edit Manager Setting

Click on any setting to change its value

![Edit Manager Setting](images/edit-manager-setting-1.png){:class='screenshot'}

* The name of the setting appears on the first line. Click the radio box in front of the value of your choice and click **Update** to change the setting value for your profile.
* Click **Back** to go back to the list of settings without making any changes.

## Notes

Settings can be added/removed by administrator in the [Default Manager Settings](default-manager-settings) screen which is placed in the Default section of the Administration menu.
