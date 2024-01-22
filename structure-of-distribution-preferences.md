---
layout: default
title: Structure of Distribution Preferences
---


* **All Classes**
	* The constraint will apply to all classes in the selected distribution set. For example, a Back-to-Back constraint among three classes seeks to place all three classes sequentially in time such that there are no intervening class times (transition time between classes is taken into account, e.g., if the first class ends at 8:20, the second has to start at 8:30).

* **Progressive**
	* The distribution constraint is created between classes in one scheduling subpart and the appropriate class(es) in one or more other subparts. This structure links child and parent classes together if subparts have been grouped. Otherwise the first class in one subpart is linked to the the first class in the second subpart, etc.

* **Groups of Two**
	* The distribution constraint is applied only on subsets containing two classes in the selected distribution set. A constraint is posted between the first two classes (in the order listed), then between the second two classes, etc.

* **Groups of Three**
	* The distribution constraint is applied only on subsets containing three classes in the selected distribution set. A constraint is posted between the first three classes (in the order listed), then between the second three classes, etc.

* **Groups of Four**
	* The distribution constraint is applied only on subsets containing four classes in the selected distribution set. A constraint is posted between the first four classes (in the order listed), then between the second four classes, etc.

* **Groups of Five**
	* The distribution constraint is applied only on subsets containing five classes in the selected distribution set. A constraint is posted between the first five classes (in the order listed), then between the second five classes, etc.

* **Pairwise**
	* The distribution constraint is created between every pair of classes in the selected distribution set. Therefore, if n classes are in the set, n(n-1)/2 constraints will be posted among the classes. This structure should not be used with "required" or "prohibited" preferences on sets containing more than a few classes.
