Vaadin provides a way of optimizing the widgetset so only the components you use are loaded to the browser. To do that you will need to provide a widgetset generator for Vaadin. Lets take a look at how we can do that:

First, we will need to provide plugin with the generator class, so in your build configuration you should add the following substituting the class name with your own:

```
vaadin {
        widgetset 'com.example.Widgetset'
        widgetsetGenerator 'com.example.WidgetsetGenerator'
}
```
The class does not need to exist, just give the class name where your want the widgetset generator to be located. A good default is to place the widgetset generator in the same package as your widgetset.

Next, we need to create the widgeset generator. To do that invoke the following task:

```
gradle createVaadinWidgetsetGenerator
```
It will create a new widgetset generator where you specified it in your build configuration.

Next you can edit the generated widgetset generator to suit your own application. More information about the different loading strategies can be found at https://vaadin.com/wiki/-/wiki/Main/Optimizing%20the%20Widget%20Set

> If you are having problems with the generator not getting applied correctly run the following task to ensure the widgetset file is up to date. ``` gradle --rerun-tasks updateWidgetset ```










