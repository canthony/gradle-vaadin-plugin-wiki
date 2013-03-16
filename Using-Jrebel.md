To use JRebel you will need a valid JRebel license and JRebel installed on your maching. See http://zeroturnaround.com/software/jrebel for instructions on license and installation.

Once you have JRebel installed locate where your rebel.jar and add the following to your gradle build script
```
vaadin{
    jrebel.enabled = true
    jrebel.location = /path/to/your/jrebel.jar
}
```
After that whenever you run your application with vaadinRun or devmode, Jrebel will be invoked automatically.
