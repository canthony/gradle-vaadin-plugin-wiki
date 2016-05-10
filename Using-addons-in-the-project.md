## Searching for addons in the directory

The first step to finding addons to add to your project is to browse the Vaadin Directory and find a suitable addon that solves your problem.

There are two ways you can find addons.

### Using the vaadin.com web site

Browse to https://vaadin.com/directory and type a search term in the search field. Once you have found an addon you like click the green *Install* button (you have to be logged in) and copy the **groupID**, **artifactId** and **version** information from the *Maven* tab. You will need it in the next step.


### Using the *vaadinAddons* task

The vaadin plugin comes with a gradle task to search for addons. 

For example to search for a QR code addon you could search by issuing 

```console
gradle vaadinAddons -Psearch=qr
```
That would return the following output
```
$ gradle vaadinAddons -Psearch=qr
:vaadinAddons
 
QRCode                        Add QR codes to your Vaadin applications           "org.vaadin.addons:qrcode:2.0.1" 

BUILD SUCCESSFUL

Total time: 1.574 secs
```

As you can see, one result was found that you can use in the project. Just as you did when using the Vaadin website, you need to copy the **groupID**, **artifactId** and **version** for later. You can find them in the 3rd column, suitable formatted as string we can later use.


## Including the addon in your build

Once you have found the addons **groupID**, **artifactId** and **version** you can add it to your build

In your build.gradle add the following:
```
dependencies {	
	compile "org.vaadin.addons:qrcode:2.0.1" 
}
```

As you notice, the dependency string is the exact same string as you get from the *vaadinAddons* task. If you are using the Vaadin Directory website you will need to construct that yourself from the **groupID**, **artifactId** and **version** you got. The format is ``<groupId>``:``<artifactId>``:``<version>``.


Other options you can use with the *vaadinAddons* task are:
- **sort** : Sort criteria (options: name,description,date,rating)
- **verbose**: Should verbose descriptions be shown


## Addons with client-side code

Some addons might include code that is executed in the browser. If that is the case the addons client side code need to be included in the projects widgetset. If you previously don't have a widgetset in your project, the plugin will create one for you called **AppWidgetset**.

If you are using *Vaadin 7.7.0+* the widgetset will automatically be detected when you start your application the next time but if you are using an older version of Vaadin you will need to add the ``@Widgetset("AppWidgetset")`` annotation to your UI class so the UI can find the new widgetset.

## Addons with custom themes

Some addons might also include a custom SASS theme. The plugin will automatically detect this and add the necessary imports into the project theme (the *addons.scss* file will be updated in your theme).