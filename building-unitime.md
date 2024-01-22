---
layout: default
title: Building UniTime
---


## Checkout


 UniTime sources can be checked out from GitHub, [https://github.com/UniTime/unitime](https://github.com/UniTime/unitime) project.
```
git clone https://github.com/UniTime/unitime.git
Cloning into 'unitime'...
remote: Counting objects: 94599, done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 94599 (delta 325), reused 362 (delta 227), pack-reused 94083
Receiving objects: 100% (94599/94599), 876.76 MiB | 6.56 MiB/s, done.
Resolving deltas: 100% (76687/76687), done.
Checking out files: 100% (3776/3776), done.
```


 Later on, it can be updated using git pull (called inside of the unitime folder)
```
cd unitime
git pull
Fast-forward
 JavaSource/org/unitime/timetable/gwt/client/sectioning/StudentSectioningWidget.java                         | 3 ++-
 JavaSource/org/unitime/timetable/gwt/client/widgets/CourseRequestBox.java                                   | 4 ++++
 JavaSource/org/unitime/timetable/onlinesectioning/custom/purdue/PurdueCourseRequestsValidationProvider.java | 9 ++++-----
 3 files changed, 10 insertions(+), 6 deletions(-)
```

## Making a build


 UniTime can be built using [Apache Ant](https://ant.apache.org/) or [Apache Maven](https://maven.apache.org/).


 1. Using Apache Ant:
```
ant
Buildfile: /Users/muller/git/unitime/build.xml
load-properties:
clean:
set-debug-mode:
set-optimize-mode:
init:
[mkdir] Created dir: /Users/muller/git/unitime/temp/build
[mkdir] Created dir: /Users/muller/git/unitime/Distributions
prepare:
[echo] Build number: 1 (dev)
[echo] Build date: Wed, 8 Aug 2018
[propertyfile] Creating new property file: /Users/muller/git/unitime/build.date
[copy] Copying 2467 files to /Users/muller/git/unitime/temp/build
compile-java:
[javac] Compiling 2368 source files to /Users/muller/git/unitime/temp/build
timetable-jar:
[jar] Building jar: /Users/muller/git/unitime/Distributions/timetable.jar
compile-gwt:
[java] Compiling module org.unitime.timetable.gwt.UniTime
[java] Compiling 20 permutations
[java] Compile of permutations succeeded
[java] Compilation succeeded -- 291.067s
[java] Linking into /Users/muller/git/unitime/temp/war/unitime
[java] Link succeeded
[java] Linking succeeded -- 4.392s
copy-libs:
[copy] Copying 85 files to /Users/muller/git/unitime/temp/war/WEB-INF/lib
[copy] Copying 10 files to /Users/muller/git/unitime/temp/war/WEB-INF
copy-jsp:
[copy] Copying 223 files to /Users/muller/git/unitime/temp/war
[copy] Copying 1 file to /Users/muller/git/unitime/Distributions
[copy] Copying 1 file to /Users/muller/git/unitime/Distributions
copy-gwt:
[copy] Copying 519 files to /Users/muller/git/unitime/temp/war
compile-war:
[copy] Copying 1 file to /Users/muller/git/unitime/temp/war/WEB-INF/lib
[jar] Building jar: /Users/muller/git/unitime/Distributions/UniTime.war
done:
[delete] Deleting directory /Users/muller/git/unitime/temp
[delete] Deleting: /Users/muller/git/unitime/build.date
build:
BUILD SUCCESSFUL
Total time: 5 minutes 33 seconds
```


 The resultant UniTime.war and timetable.jar files are located in the unitime/Distributions folder.


 2. Using Apache Maven:
```
mvn package
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------< org.unitime:unitime >-------------------------
[INFO] Building UniTime 4.3
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- buildnumber-maven-plugin:1.1:create (default) @ unitime ---
[INFO] Checking for local modifications: skipped.
[INFO] Updating project files from SCM: skipped.
[INFO] Executing: /bin/sh -c cd /Users/muller/git/unitime && git rev-parse --verify HEAD
[INFO] Working directory: /Users/muller/git/unitime
[INFO] Storing buildNumber: dc9f0375600ea9d19c81b9c0bccdc3b43bbfecd9 at timestamp: 1533728860442
[INFO] Executing: /bin/sh -c cd /Users/muller/git/unitime && git rev-parse --verify HEAD
[INFO] Working directory: /Users/muller/git/unitime
[INFO] Storing buildScmBranch: UNKNOWN
[INFO]
[INFO] --- maven-antrun-plugin:1.7:run (default) @ unitime ---
[WARNING] Parameter tasks is deprecated, use target instead
[INFO] Executing tasks
main:
[INFO] Executed tasks
[INFO]
[INFO] --- maven-resources-plugin:2.5:resources (default-resources) @ unitime ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 2 resources to /Users/muller/git/unitime/target/src
[INFO] Copying 2361 resources to /Users/muller/git/unitime/target/src
[INFO] Copying 242 resources
[INFO]
[INFO] --- maven-compiler-plugin:2.5.1:compile (default-compile) @ unitime ---
[INFO] Compiling 2363 source files to /Users/muller/git/unitime/target/classes
[INFO]
[INFO] --- maven-resources-plugin:2.5:testResources (default-testResources) @ unitime ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/muller/git/unitime/src/resources
[INFO]
[INFO] --- maven-compiler-plugin:2.5.1:testCompile (default-testCompile) @ unitime ---
[INFO] No sources to compile
[INFO]
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ unitime ---
[INFO] No tests to run.
[INFO]
[INFO] --- gwt-maven-plugin:2.8.2:compile (default) @ unitime ---
[INFO] Compiling module org.unitime.timetable.gwt.UniTime
[INFO] Compiling 20 permutations
[INFO] Compile of permutations succeeded
[INFO] Compilation succeeded -- 341.363s
[INFO] Linking into /Users/muller/git/unitime/target/gwt/unitime
[INFO] Link succeeded
[INFO] Linking succeeded -- 5.023s
[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ unitime ---
[INFO] Building jar: /Users/muller/git/unitime/target/unitime-4.3.jar
[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default) @ unitime ---
[INFO]
[INFO] --- maven-war-plugin:2.2:war (war) @ unitime ---
[INFO] Packaging webapp
[INFO] Assembling webapp [unitime] in [/Users/muller/git/unitime/target/unitime-4.3]
[INFO] Processing war project
[INFO] Copying webapp webResources [/Users/muller/git/unitime/WebContent] to [/Users/muller/git/unitime/target/unitime-4.3]
[INFO] Copying webapp webResources [/Users/muller/git/unitime/target/gwt] to [/Users/muller/git/unitime/target/unitime-4.3]
[INFO] Webapp assembled in [8439 msecs]
[INFO] Building war: /Users/muller/git/unitime/target/UniTime.war
[INFO] WEB-INF/web.xml already added, skipping
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 06:49 min
[INFO] Finished at: 2018-08-08T13:54:28+02:00
[INFO] ------------------------------------------------------------------------
```


 The resultant UniTime.war and timetable.jar files are located in the unitime/target folder.

## Updating UniTime with a new build 

* To upgrade an existing UniTime installation, only the new **UniTime.war** file should be placed in the Tomcat/webapps folder instead of the existing one. All the necessary changes to the database are done automatically during the first deployment. The safest way to do so is as follows:
	1. Stop Tomcat
	2. Backup the existing database (e.g., using [mysqldump](http://dev.mysql.com/doc/refman/5.5/en/mysqldump.html) on MySQL or [exp](http://wiki.oracle.com/page/Oracle+export+and+import+) on Oracle)
	3. In Tomcat/webapps, remove UniTime folder and replace the existing UniTime.war with the new one
	4. Delete the content of Tomcat/work folder.
	5. Start Tomcat

* If you are using remove solver servers, the appropriate JARs needs to be updated as well.

## Notes


 The master branch usually contains the latest development version (UniTime 4.8) at the moment. Older versions are placed on maint_XXX branches (e.g., maint_UniTime47 for UniTime 4.7), and development versions are on the dev_XXX branches (e.g., dev_UniTime44 for UniTime 4.4).
