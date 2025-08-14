---
layout: default
title: Test HQL
---


## Screen Description

The Test HQL screen is a place to enter an [HQL](https://docs.jboss.org/hibernate/orm/6.6/querylanguage/html_single/Hibernate_Query_Language.html) query which uses the timetabling database and see the results of such query.

![Test HQL](images/test-hql-1.png){:class='screenshot'}

This page offers a place where HQL queries can be tested before they are turned into custom [HQL Reports](hql-reports).

**Note:** If `%SESSION%` is used in the query, it will get automatically replaced by the unique ID of the current academic session. There are no other parameters available.

## Details

* **Query**
	* Enter the HQL query you need

* **Result**
	* The resulting table

## Operations

* **Submit**
	* Submit the query

* **Clear Cache**
	* Clear Hibernate L2 cache

* **Export CSV**
	* Export the resulting data in a CSV format

## Examples
```
select s from Session s
```

```
select t from TimePattern t where t.session.academicTerm='Fal' and t.session.academicYear='2007'
```

```
select c from Class_ c inner join c.schedulingSubpart.instrOfferingConfig.instructionalOffering.courseOfferings co
  where co.isControl=true and co.subjectArea.subjectAreaAbbreviation='BIOL'
```

## Notes

* You can find HQL documentation at [https://hibernate.org/orm/documentation/6.6](https://docs.jboss.org/hibernate/orm/6.6/querylanguage/html_single/Hibernate_Query_Language.html)

* Timetabling hibernate model XML files can be found at [https://github.com/UniTime/unitime/tree/master/JavaSource](https://github.com/UniTime/unitime/tree/master/JavaSource)
