*Originally posted on http://devsoap.com/converting-a-vaadin-maven-project-to-gradle*
-

So you started out with creating a new Vaadin project in Eclipse and it created a Maven project and after a while you have noticed it isn't working out for you and want to switch to Gradle to make your life easier.

The good news is that Gradle provides great tooling for upgrading your project from Maven to Gradle and with the *Gradle Vaadin plugin* you will be happily running with Gradle in no time.

To demonstrate the approach I have taken the Vaadin Spreadsheet tutorial provided by **Vaadin** over at https://github.com/vaadin/spreadsheet-tutorial. It is a typical Vaadin application with some addons, widgetset compilation and custom theme.

#### Setting the project up for conversion
The first thing we need to do is checkout the project from Git. You can do that by issuing the following command:
```console
$ git clone https://github.com/vaadin/spreadsheet-tutorial.git
```

That will clone the project and you should see the following file structure:
```console
$ tree
.
├── pom.xml
├── README.md
├── Simple Invoice.xlsx
└── src
    └── main
        ├── java
        │   └── com
        │       └── vaadin
        │           └── MyUI.java
        ├── resources
        │   └── com
        │       └── vaadin
        │           └── MyAppWidgetset.gwt.xml
        └── webapp
            └── VAADIN
                └── themes
                    └── mytheme
                        ├── addons.scss
                        ├── favicon.ico
                        ├── mytheme.scss
                        └── styles.scss

12 directories, 9 files
```
That looks like a very typical Vaadin project!

#### Converting to a Gradle project

The thing that defines this project as a Maven project is that this project has a *pom.xml* file. What we would like to do is convert that file to a corresponding *build.gradle* and *settings.gradle* file which defines a Gradle project.

Of course we could do that by hand, but that would be tedious and error prone and we as developers like neither of those. So instead, by executing the following command in the root directory of the project *Gradle* will do that for us!

```console
$ gradle init
```

After you have executed that you should see some new files in your project:
```console
$ tree
.
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── pom.xml
├── README.md
├── settings.gradle
├── Simple Invoice.xlsx
└── src
    └── main
        ├── java
        │   └── com
        │       └── vaadin
        │           └── MyUI.java
        ├── resources
        │   └── com
        │       └── vaadin
        │           └── MyAppWidgetset.gwt.xml
        └── webapp
            └── VAADIN
                └── themes
                    └── mytheme
                        ├── addons.scss
                        ├── favicon.ico
                        ├── mytheme.scss
                        └── styles.scss

14 directories, 15 files
```
When you run *init* Gradle will recognize that this project is a Maven project, analyze your *pom.xml* file and create the corresponding Gradle files for you! It will also set you up the the Gradle Wrapper that will allow developers who haven't installed Gradle on their system to run the the build.

#### Making the project a *Vaadin* Gradle project

While *init* will do the grunt work of converting the project to a valid Gradle project and set up the dependencies correctly, we still need to set up the *Vaadin* specific things like widgetset compilation and theme compilation. 

To do that lets have a look at the *build.gradle* file that was generated
```groovy
apply plugin: 'java'
apply plugin: 'maven'

group = 'com.vaadin'
version = '1.0-SNAPSHOT'

description = """spreadsheet-tutorial"""

sourceCompatibility = 1.7
targetCompatibility = 1.7

repositories {
     maven { url "http://maven.vaadin.com/vaadin-addons" }
     maven { url "https://oss.sonatype.org/content/repositories/vaadin-snapshots/" }
     maven { url "http://repo.maven.apache.org/maven2" }
}
dependencies {
    compile group: 'com.vaadin', name: 'vaadin-server', version:'7.6.4'
    compile group: 'com.vaadin', name: 'vaadin-push', version:'7.6.4'
    compile group: 'com.vaadin', name: 'vaadin-themes', version:'7.6.4'
    compile group: 'com.vaadin.addon', name: 'vaadin-spreadsheet', version:'1.2.0.alpha1'
    providedCompile group: 'javax.servlet', name: 'javax.servlet-api', version:'3.0.1'
    providedCompile group: 'com.vaadin', name: 'vaadin-client', version:'7.6.4'
}
```
 
Lets now go through this piece-by-piece and update the necessary parts

Lets first start with the applied Gradle plugins. Lets convert this
```groovy
apply plugin: 'java'
apply plugin: 'maven'
```
into 
```groovy
plugins {
  id "fi.jasoft.plugin.vaadin" version "0.11"
}
```
**Whoaw**, what happened here?! 

This is where the magic happens, instead of just applying the *java* plugin we now apply the Gradle Vaadin plugin, effectively making this project a Vaadin project. The Vaadin plugin will handle a lot of things for us and simplify our build script. 

We also removed the **maven** plugin. You might want to keep it if you have third-party Maven repositories you need to include. In the particular project there are no custom repositories needed so we can just remove it.

Next, we can totally remove the following repositories definition:
```groovy
repositories {  
     maven { url "http://maven.vaadin.com/vaadin-addons" }
     maven { url "https://oss.sonatype.org/content/repositories/vaadin-snapshots/" }
     maven { url "http://repo.maven.apache.org/maven2" }
}
```
The *Gradle Vaadin Plugin* will provide all of these repositories automatically for us so there is no need to duplicate them here. So we can just remove the whole ``repositories { ... }`` definition from the build file.

Next up the dependencies section
```groovy
dependencies {  
    compile group: 'com.vaadin', name: 'vaadin-server', version:'7.6.4'
    compile group: 'com.vaadin', name: 'vaadin-push', version:'7.6.4'
    compile group: 'com.vaadin', name: 'vaadin-themes', version:'7.6.4'
    compile group: 'com.vaadin.addon', name: 'vaadin-spreadsheet', version:'1.2.0.alpha1'
    providedCompile group: 'javax.servlet', name: 'javax.servlet-api', version:'3.0.1'
    providedCompile group: 'com.vaadin', name: 'vaadin-client', version:'7.6.4'
}
```
can be replaced by
```groovy
dependencies {  
    compile group: 'com.vaadin.addon', name: 'vaadin-spreadsheet', version:'1.2.0.alpha1'
}

vaadin {
    version '7.6.4'
}

```
Again, the *Gradle Vaadin Plugin* will automatically include the necessary dependencies for Vaadin so the only dependency we are left with is the addon dependency to *Vaadin Spreadsheet*.

I also add the ```vaadin {...}``` configuration to keep the Vaadin version used by the project the same as the previous Maven build used. The *version* can be omitted if you want, in that case the latest stable version of Vaadin will be used. 

The final version of the **build.gradle** file should look like this:
```groovy
plugins {  
  id "fi.jasoft.plugin.vaadin" version "0.11"
}

group = 'com.vaadin'
version = '1.0-SNAPSHOT'

description = """spreadsheet-tutorial"""

sourceCompatibility = 1.7
targetCompatibility = 1.7

dependencies {
    compile group: 'com.vaadin.addon', name: 'vaadin-spreadsheet', version:'1.2.0.alpha1'
}

vaadin {
    version '7.6.4'
}
```
**And that is it!** 

Once you've done this the project can be run by invoking the following, just like you previously used *jetty:run* with maven.
```console
$ gradle vaadinRun
```

The whole resulting project can be found at https://github.com/johndevs/spreadsheet-tutorial-gradle which you can clone and directly run if wish.