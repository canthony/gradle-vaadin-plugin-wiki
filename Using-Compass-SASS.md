By default all the SASS files in a Vaadin project are compiled with the Vaadin Sass compiler. In 90% of the cases this is most likely very sufficient and I would recommend staying with it if your don't have a special need not to.

However, some designers might be using features of SASS that has not yet been implemented in Vaadin's compiler and so the plugin now also supports switching to Compass SASS easily by only setting 

```groovy
vaadinThemeCompile.compiler = 'compass'.
```

However, you are paying for these extra features with your build performance as the Compass compiler is significantly slower than the Vaadin compiler. I've written previously more about this is http://devsoap.com/gradle-vaadin-plugin-0-11-sneak-peak/ so if you are considering taking Compass into use, please read though the article first.