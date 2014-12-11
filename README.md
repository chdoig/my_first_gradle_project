Gradle:

# Case 1: If you are starting a brand new gradle project
# Go download gradle from: 
mkdir temp-gradle
cd temp-gradle
# Initialize a git repo
git init
# `brew install wget` if you don't have wget. (Alternative curl)
wget https://services.gradle.org/distributions/gradle-2.2.1-bin.zip
# unzip it to a place
unzip gradle-2.2.1-bin.zip

```bash
cd gradle-2.2.1
cd bin/
# Check that you have the correct version
./gradle --version
```
or

from the project directory run:
```bash
temp-gradle/gradle-2.2.1/bin/gradle wrapper
```

# Now you have the gradle wrapper installed for the current project (a script and a jar file)
./gradlew --version
# That's going to download gradle-2.2.1 (again...) to your user directory in a place the wrapper can find. 
# Note: It won't download it again if it's already in that place.
# At this point running ./gradlew will run gradle from now on. 

git add gradlew
git add gradlew.bat 
git add gradle/

git commit -m "Add the Gradle wrapper"

# Write your build.gradle file
vim build.gradle

```groovy
apply plugin: 'java'
apply plugin: 'idea'


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

mkdir -p src/main/java

# This is where all your Java source goes

```java
public class HelloWorld {

    public static void main(String[] args) {
        System.out.println("Hello, World");
    }

}
```
# Generate idea project files
./gradlew idea

# Now you can open your project's .ipr in IntelliJ

