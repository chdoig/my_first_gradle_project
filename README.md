# A basic introduction to Gradle

# Starting a brand new gradle project

The first time you use Gradle, you'll have to download it. After that, the gradle wrapper can bootstrap itself,
so you can just copy the gradle/wrapper folder into your next repository.

We can save this first gradle download in a temporary folder.

```bash
mkdir temp-gradle
cd temp-gradle
```

Note: In OSX, `brew install wget` if you don't have wget. (Or, alternatively, curl)

```bash
wget https://services.gradle.org/distributions/gradle-2.2.1-bin.zip
# unzip it
unzip gradle-2.2.1-bin.zip
```

From the project directory run:

```bash
temp-gradle/gradle-2.2.1/bin/gradle wrapper
```
This creates the gradle wrapper task, which generates `gradlew`, `gradlew.bat`, `gradle/`, in your repository.

Now you have the gradle wrapper installed for the current project (a script and a jar file)

```bash
./gradlew --version
```

That's going to download gradle-2.2.1 (again...) to your user directory in a place the wrapper can find.
Note: It won't download it again if it's already in that place.
At this point running ./gradlew will run gradle from now on.

We want to add those files in our repository.

```bash
git add gradlew
git add gradlew.bat 
git add gradle/
git commit -m "Add the Gradle wrapper"
```

Write your build.gradle file

```bash
vim build.gradle
```
E.g. a simple example of a build.gradle:

```groovy
apply plugin: 'java'
apply plugin: 'idea'
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'

repositories {
    mavenCentral()
}

dependencies {
    compile "com.google.guava:guava:18.0"

    // junit testing
    testCompile "junit:junit:4.11"
    testCompile "org.mockito:mockito-all:1.9.5"
}
```

We also create a "Hello World" Java project and include a random dependency.

mkdir -p src/main/java

vim src/main/java/HelloWorld.java

```java
package hello;

import com.google.common.collect.Lists;

public class HelloWorld {

    public static void main(String[] args) {
        Lists.newArrayList();
        System.out.println("Hello, World");
    }

}
```

[SO: Creating Runnable Jar with Gradle](http://stackoverflow.com/questions/21721119/creating-runnable-jar-with-gradle)

>The application plugin provides an alternate approach; instead of creating an executable JAR, it provides:
>
>a run task to facilitate easily running the application directly from the build
>an installApp task that generates a directory structure including the built JAR, all of the JARs that it depends on, and a startup script that pulls it all together into a program you can run
>distZip and distTar tasks that create archives containing a complete application distribution (startup scripts and JARs)

If we run:

```bash
$ ./gradlew tasks

```

We get all the available runnable tasks from the root project:

```bash
:tasks

------------------------------------------------------------
All tasks runnable from root project
------------------------------------------------------------

Application tasks
-----------------
distTar - Bundles the project as a JVM application with libs and OS specific scripts.
distZip - Bundles the project as a JVM application with libs and OS specific scripts.
installApp - Installs the project as a JVM application along with libs and OS specific scripts.
run - Runs this project as a JVM application

Build tasks
-----------
assemble - Assembles the outputs of this project.
build - Assembles and tests this project.
buildDependents - Assembles and tests this project and all projects that depend on it.
buildNeeded - Assembles and tests this project and all projects it depends on.
classes - Assembles classes 'main'.
clean - Deletes the build directory.
jar - Assembles a jar archive containing the main classes.
testClasses - Assembles classes 'test'.

Build Setup tasks
-----------------
init - Initializes a new Gradle build. [incubating]
wrapper - Generates Gradle wrapper files. [incubating]

Documentation tasks
-------------------
javadoc - Generates Javadoc API documentation for the main source code.

Help tasks
----------
components - Displays the components produced by root project 'my_first_gradle_project'. [incubating]
dependencies - Displays all dependencies declared in root project 'my_first_gradle_project'.
dependencyInsight - Displays the insight into a specific dependency in root project 'my_first_gradle_project'.
help - Displays a help message.
projects - Displays the sub-projects of root project 'my_first_gradle_project'.
properties - Displays the properties of root project 'my_first_gradle_project'.
tasks - Displays the tasks runnable from root project 'my_first_gradle_project'.

IDE tasks
---------
cleanIdea - Cleans IDEA project files (IML, IPR)
idea - Generates IDEA project files (IML, IPR, IWS)

Verification tasks
------------------
check - Runs all checks.
test - Runs the unit tests.

Other tasks
-----------
cleanIdeaWorkspace

Rules
-----
Pattern: clean<TaskName>: Cleans the output files of a task.
Pattern: build<ConfigurationName>: Assembles the artifacts of a configuration.
Pattern: upload<ConfigurationName>: Assembles and uploads the artifacts belonging to a configuration.

To see all tasks and more detail, run with --all.

BUILD SUCCESSFUL

Total time: 2.803 secs
```


Some nice tasks from the application plugin:

distTar - Bundles the project as a JVM application with libs and OS specific scripts.
distZip - Bundles the project as a JVM application with libs and OS specific scripts.
dependencies - Displays all dependencies declared in root project 'my_first_gradle_project'.
build - Assembles and tests this project.

To assemble and test the project:

```bash
./gradlew clean build
```

To bundle the project as a JVM application in a zip file under `/build/distributions`:

```bash
./gradlew distZip
```

To see all your project dependencies:

```bash
./gradlew dependencies
```

```bash
:dependencies

------------------------------------------------------------
Root project
------------------------------------------------------------

archives - Configuration for archive artifacts.
No dependencies

compile - Compile classpath for source set 'main'.
\--- com.google.guava:guava:18.0

default - Configuration for default artifacts.
\--- com.google.guava:guava:18.0

runtime - Runtime classpath for source set 'main'.
\--- com.google.guava:guava:18.0

testCompile - Compile classpath for source set 'test'.
+--- com.google.guava:guava:18.0
+--- junit:junit:4.11
|    \--- org.hamcrest:hamcrest-core:1.3
\--- org.mockito:mockito-all:1.9.5

testRuntime - Runtime classpath for source set 'test'.
+--- com.google.guava:guava:18.0
+--- junit:junit:4.11
|    \--- org.hamcrest:hamcrest-core:1.3
\--- org.mockito:mockito-all:1.9.5

BUILD SUCCESSFUL

Total time: 2.345 secs
```




