By default all the SASS files in a Vaadin project are compiled with the Vaadin Sass compiler. In 90% of the cases this is most likely very sufficient and I would recommend staying with it if your don't have a special need not to.

However, some designers might be using features of SASS that has not yet been implemented in Vaadin's compiler and so the plugin now also supports switching to Compass SASS easily by only setting 

```groovy
vaadinThemeCompile.compiler = 'compass'
```

Or to compile with **libSass** you can use:

```groovy
vaadinThemeCompile.compiler = 'libsass'
```