---
layout: default
title: Eclipse
---

### Table of Contents
{:.no_toc}
* table
{:toc}

## Install Eclipse IDE

Download and install Eclipse IDE for Enterprise Java and Web Developers (Eclipse IDE 2026-06), e.g., from [eclipse.org/downloads/packages](https://www.eclipse.org/downloads/packages/) using the Eclipse Installer

![Eclipse](images/eclipse-1.png){:class='screenshot small'}

## Create UniTime project

If you plan to make changes, you should consider forking the [UniTime](https://github.com/UniTime/unitime) project first. See [Fork A Repo](https://help.github.com/articles/fork-a-repo/) for more details.

* File > Import, select Git > Project from Git, Next
* Select "Clone URI" and click Next
	* **Note:** Use "Existing local repository" if you already have the UniTime project cloned somewhere, e.g., using the [GitHub Desktop](https://desktop.github.com/) app or the [git](https://git-scm.com/docs/git) command line tool
* Enter "https://github.com/UniTime/unitime.git" as URI; the rest should auto-populate from the URL, click Next
	* Or, you can use "git@github.com:UniTime/unitime.git" as URI and generate an SSH key (see [Generating SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) for more details)
	* If you have forked the unitime repository, the URI will be different
* Click Deselect All and select the master and the maintenance branches you want/need (if any).
* Click Next
* Once cloned, hit Next (import existing Eclipse projects) and Finish

![Eclipse](images/eclipse-2.png){:class='screenshot small'}


![Eclipse](images/eclipse-3.png){:class='screenshot small'}


![Eclipse](images/eclipse-4.png){:class='screenshot small'}


![Eclipse](images/eclipse-5.png){:class='screenshot small'}


![Eclipse](images/eclipse-6.png){:class='screenshot small'}


![Eclipse](images/eclipse-7.png){:class='screenshot small'}


![Eclipse](images/eclipse-8.png){:class='screenshot small'}


![Eclipse](images/eclipse-9.png){:class='screenshot small'}

### Install GWT Eclipse Plugin

* Help > Install New Software...
* Click Add, Name: GWT Plugin, Location: https://plugins.gwtproject.org/eclipse/gwt-eclipse-plugin/4.2.0, OK
* Select GWT Eclipse Plugin
* Follow the installation instructions, accept the license, and at the end, click Restart Eclipse
	* If there is a warning about installing software that contains unsigned content, click OK


![Eclipse](images/eclipse-10.png){:class='screenshot small'}

* Download the GWT (e.g., GWT 2.13.0) from [gwtproject.org/download.html](http://www.gwtproject.org/download.html) and unzip it.
	* **Important:** The version should match the version used in UniTime (see the version of the gwt-dev-xxx.jar under the 3rd_party, e.g., gwt-dev-2.13.0.jar)

* In Eclipse, open File > Properties, select GWT > GWT Settings, click Add
* Select a directory that has an unzipped distribution of GWT 2.13.0, hit OK
* Select the newly added GWT 2.13.0 as the default, click OK


![Eclipse](images/eclipse-11.png){:class='screenshot small'}


![Eclipse](images/eclipse-12.png){:class='screenshot small'}

* Right-click on the UniTime project, click Properties, select GWT > Web Application, toggle "This project has a WAR directory", set WAR directory to "WebContent" and click OK


![Eclipse](images/eclipse-13.png){:class='screenshot small'}

* Under the GWT > General Settings, make sure that the installed GWT SDK is being used (Use specific SDK option).

![Eclipse](images/eclipse-27.png){:class='screenshot small'}

### Additional Eclipse Configuration

* Right-click on the UniTime project, click Properties
* Select Project Facets, make sure that Dynamic Web Module (**version 4.0**), GWT, and Java (**version 17**) are selected, click Apply


![Eclipse](images/eclipse-14.png){:class='screenshot small'}


* Under the GWT > Facet Settings, make sure that the Super Development Mode is not checked.

![Eclipse](images/eclipse-28.png){:class='screenshot small'}

* Select Deployment Assembly, and update the screen to look like this, hit Apply
	* /JavaSouce deploys as WEB-INF/classes
	* /WebContent deploys as /


![Eclipse](images/eclipse-15.png){:class='screenshot small'}

## Setup Apache Tomcat

This guide expects that you already have the Apache Tomcat downloaded and installed somewhere.

* Including the MySQL Connector/J driver in Tomcat/lib, see [UniTime Installation](installation).

### Setup JRE and its parameters

* Open File > Properties, select Java > Installed JREs, click Edit
* Put in the following Default VM arguments, hit Finish

	```-Xmx2g```

* You can also include a path to the UniTime custom.properties file if needed

	```-Dtmtbl.custom.properties=/path/to/custom.properties```


![Eclipse](images/eclipse-16.png){:class='screenshot small'}


![Eclipse](images/eclipse-17.png){:class='screenshot small'}

### Create Apache Tomcat v10.1 server configuration

* Open File > Properties, select Server > Runtime Environments, click Add
* Select Apache Tomcat v10.1, check the "Create a new local server", click Next
* Select Tomcat installation directory, hit Finish


![Eclipse](images/eclipse-18.png){:class='screenshot small'}


![Eclipse](images/eclipse-19.png){:class='screenshot small'}


![Eclipse](images/eclipse-20.png){:class='screenshot small'}

### Compile GWT

* Right click on the UniTime project, select GWT, click on Compile
* Make sure that either UniTimeDev (fewer permutations) or UniTime (all permutations) but not both is on the Entry Point Modules list, click Compile
* If asked, select WebContent as the WAR directory

![Eclipse](images/eclipse-21.png){:class='screenshot small'}


![Eclipse](images/eclipse-22.png){:class='screenshot small'}

### Deploy UniTime

* On the Servers tab, double-click Tomcat v10.1 Server at localhost
* On the Overview tab, set Deploy path to webapps and increase the start and stop Timeouts
* On the Modules tab, hit Add Web Module, select UniTime and hit OK
* Save changes


![Eclipse](images/eclipse-23.png){:class='screenshot small'}


![Eclipse](images/eclipse-24.png){:class='screenshot small'}


![Eclipse](images/eclipse-25.png){:class='screenshot small'}

### Start the Tomcat

* On the Servers tab, select Tomcat v10.1 and click the debug (little green bug) or start (green round icon with a triangle in it) 
* Check the Console tab for any errors


![Eclipse](images/eclipse-26.png){:class='screenshot small'}
