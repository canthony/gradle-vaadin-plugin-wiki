### Installing Gradle support in Eclipse
As of writing the Eclipse Gradle support is only bundled with the Java, Committer and RAP/RCP distributions of Eclipse Neon which means that if you are a Vaadin developer you most likely have the Java EE version and will need to manually install the Gradle support. Hopefully this will change in the future.

To install the Gradle support in Eclipse we need to install a eclipse plugin called Gradle BuildShip which is the official Gradle support provided by the Eclipse Foundation. We can do that from the Eclipse Marketplace by searching for “buildship” and pressing install.

![Eclipse Marketplace Install Buildship](images/eclipse-marketplace-install-buildship.png)

### Creating a Vaadin Gradle Project

To create a Gradle project, we will use the Gradle Project wizard. 

So Select **File -> New -> Other -> Gradle -> Gradle Project** and select *Next*.

![New Gradle Project Wizard](images/eclipse-new-gradle-project-wizard.png) 

After you have select Next, there will be a short introduction screen presenting the features of the Gradle integration, whereafter if you click Next you will be asked to enter a name for your project. 

After you’ve entered the name select Next again, and the last page of the wizard will be displayed with some options how to handle the Gradle version. You can ignore these for now and just go with the recommended option and click Finish and the project will be created for you.

After you have created the project there will be some placeholder classes and an example **build.gradle** file created for you. We don’t need any of it, so you can just go ahead and remove the src-folder and empty the **build.gradle** file so it is just an empty file. 

To make the project a Vaadin project we need to add a Vaadin plugin to our build file. This can be done by adding the following snippet to your **build.gradle**:
