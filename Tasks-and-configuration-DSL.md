## Main configuration
* ``vaadin.version`` - Vaadin version. Defaults to latest Vaadin 7
* ``vaadin.manageDependencies`` - Should the plugin manage the Vaadin depencies for you. Default is true.
* ``vaadin.manageRepositories`` - Should the plugin add repositories such as maven central and vaadin addons to the project.  Default is true.
* ``vaadin.mainSourceSet`` - Defines the main source set where all source files will be generated.
* ``vaadin.push`` - Should vaadin push be enabled for the application. Default is false.
* ``vaadin.logToConsole`` - Output server logs to console instead of to file. Default is false.

# Addon configurations
* ``vaadin.addon.author`` - The author of the Vaadin addon.
* ``vaadin.addon.license`` - The licence of the Vaadin addon.
* ``vaadin.addon.title`` - The title for the addon as seen in the Vaadin Directory.
* ``vaadin.addon.styles`` - An array of paths relative to webroot (eg. '/VAADIN/addons/myaddon/myaddon.scss') where CSS and SCSS files for an addon can be found.

# Plugin tasks

## vaadinCreateComponent

Creates a new Vaadin Component

### Parameters 
*  ``name`` - The class name of the component. By default *MyComponent*.

## vaadinCreateComposite

Creates a new Vaadin Composite.

### Parameters
* ``name`` -  The class name of the composite. By default *MyComposite*.
* ``package`` - The package where the composite should be placed. By default *com.example.\<component name\>*. 

## vaadinCreateProject

Creates a new Vaadin Project.

### Parameters
* ``name`` -  The application name. By default the project name.
* ``package`` - The package where the application classes will be placed. 
* ``widgetset`` - The widgetset name, if applicable.
By default, if a widgetset is defined, that package is used, otherwise *com.example.\<project name\>* is used.

## vaadinCreateAddonProject

Creates a new Vaadin Project to build an addon for the Vaadin Directory.

## vaadinCreateTheme

Creates a new Vaadin Theme.

### Parameters
* ``name`` -  The name of the theme. By default the project name.

## vaadinCreateAddonTheme

Creates a new theme for a Vaadin Addon project.

### Parameters
* ``name`` -  The name of the theme. By default, if the addon title is used to generated the theme name, 
otherwise *MyAddonTheme* is used.

## vaadinCreateWidgetsetGenerator

Creates a new widgetset generator for optimizing the widgetset

## vaadinCreateTestbenchTest

Creates a new Testbench test.

## Parameters
* ``name`` -  The test class name.
* ``package`` - The test class package.

## vaadinDevMode (Deprecated)

Run Development Mode for easier debugging and development of client widgets.

Deprecated in favor of **vaadinSuperDevMode**

### Configurations
* ``noserver`` - Should the internal server be used. Default *false*.
* ``bindAddress`` - To what host or ip should development mode bind itself to. By default *localhost*.
* ``codeServerPort`` - To what port should development mode bind itself to. By default *9997*.
* ``extraArgs`` - Extra arguments passed to the code server. By default *none*.
* ``logLevel`` - The log level. Possible levels NONE,DEBUG,TRACE,INFO. By default *INFO*.
* ``server`` - Application server to use. Possible application servers are 'payara', 'jetty'. Default is *payara*.
* ``debug`` - Should application be run in debug mode. When running in production set this to true. Default is *true*.
* ``debugPort`` - The port the debugger listens to. Default is 8000.
* ``jvmArgs`` - Extra jvm args passed to the JVM running the Vaadin application.
* ``serverRestart`` - Should the server restart after every change. By default *true*.
* ``serverPort`` - The port the vaadin application should run on. By default 8080.
* ``themeAutoRecompile`` -  Should theme be recompiled when SCSS file is changes. Default is *true*.
* ``openInBrowser`` - Should the application be opened in a browser when it has been launched. By defailt *true*.

## vaadinSuperDevMode

Run Super Development Mode for easier client widget development.

### Configurations
* ``noserver`` - Should the internal server be used. Default *false*.
* ``bindAddress`` - To what host or ip should development mode bind itself to. By default *localhost*.
* ``codeServerPort`` - To what port should development mode bind itself to. By default *9997*.
* ``extraArgs`` - Extra arguments passed to the code server. By default *none*.
* ``logLevel`` - The log level. Possible levels NONE,DEBUG,TRACE,INFO. By default *INFO*.
* ``server`` - Application server to use. Possible application servers are 'payara', 'jetty'. Default is *payara*.
* ``debug`` - Should application be run in debug mode. When running in production set this to true. Default is *true*.
* ``debugPort`` - The port the debugger listens to. Default is 8000.
* ``jvmArgs`` - Extra jvm args passed to the JVM running the Vaadin application.
* ``serverRestart`` - Should the server restart after every change. By default *true*.
* ``serverPort`` - The port the vaadin application should run on. By default 8080.
* ``themeAutoRecompile`` -  Should theme be recompiled when SCSS file is changes. Default is *true*.
* ``openInBrowser`` - Should the application be opened in a browser when it has been launched. By defailt *true*.

## vaadinCompile

Compiles Vaadin Addons and components into Javascript.

### Configurations
* ``style`` - Compilation style. By default *OBF*.
* ``optimize`` - Should the compilation result be optimized. By default *0*.
* ``logging`` - Should logging be enabled. By default *true*.
* ``logLevel`` - The log level. Possible levels NONE,DEBUG,TRACE,INFO. By default *INFO*.
* ``localWorkers`` - Amount of local workers used when compiling. By default the amount of processors.
* ``draftCompile`` - Should draft compile be used. By default *true*.
* ``strict`` - Should strict compiling be used. By default *true*.
* ``userAgent`` - What user agents (browsers should be used. By defining null all user agents are used.)
* ``jvmArgs`` - Extra jvm arguments passed the JVM running the compiler
* ``extraArgs`` - Extra arguments passed to the compiler
* ``sourcePaths`` - Source paths where the compiler will look for source files. By default *['client', 'shared']*.
* ``collapsePermutations`` - Should the compiler permutations be collapsed. By default *true*.
* ``extraInherits`` - Extra module inherits.
* ``gwtSdkFirstInClasspath`` - Should GWT be placed first in the classpath when compiling the widgetset. By default *true*.
* ``outputDirectory`` - (Optional) root directory, for generated files; default is the web-app dir from the WAR plugin
* ``widgetsetCDN`` - Use external Vaadin hosted CDN for compiling the widgetset. By default *false*.
* ``profiler`` - Should the Vaadin client side profiler be used. By defailt *false*.
* ``manageWidgetset`` - Should the plugin manage the widgetset (gwt.xml file). By default *true*.
* ``widgetset`` - The widgetset to use for the project. Leave empty for a pure server side project, or to autodetect widgetset.
* ``widgetsetGenerator`` - The widgetset generator to use.

## vaadinThemeCompile

Compiles a Vaadin SASS theme into CSS.

### Configurations
* ``compiler`` - The SASS compiler to use. *vaadin*,*compass* and *libsass* are available. *vaadin* is default.
* ``themesDirectory`` - Root directory for themes. By default *src/main/webapp/VAADIN/themes*

## vaadinRun

Runs the Vaadin application on the application server.

### Parameters
* ``stopAfterStart`` - Should the server stop after starting. By default *false*.
* ``nobrowser`` - Do not open browser after server has started. By default *true*.

### Configurations
* ``server`` - Application server to use. Possible application servers are 'payara', 'jetty'. Default is *payara*.
* ``debug`` - Should application be run in debug mode. When running in production set this to true. Default is *true*.
* ``debugPort`` - The port the debugger listens to. Default is 8000.
* ``jvmArgs`` - Extra jvm args passed to the JVM running the Vaadin application.
* ``serverRestart`` - Should the server restart after every change. By default *true*.
* ``serverPort`` - The port the vaadin application should run on. By default 8080.
* ``themeAutoRecompile`` -  Should theme be recompiled when SCSS file is changes. Default is *true*.
* ``openInBrowser`` - Should the application be opened in a browser when it has been launched. By defailt *true*.
* ``classesDir`` - The directory where the compiled application classes are located. Default is project.sourceSets.main.output.classesDir.

## vaadinAddons

Search for addons in the Vaadin Directory.

### Parameters
* ``search`` - String to search for in addons. By default empty string returning all addons in the directory.
* ``sort`` - Sort criteria (options: name,description,date,rating). By default *unsorted*.
* ``verbose`` - Should verbose descriptions be shown. By default *false*.

## vaadinTestbench

### Configurations
* ``enabled`` - Should Testbench be enabled when running tests. Default is *false*.
* ``version`` - What version of testbench should be used. Default is *3.+*
* ``runApplication`` - Should the application be run before tests are run. Default is *true*.

## vaadinTestbenchHub

### Configurations
* ``enabled`` - Should the testbench hub be enabled when tests are run. Default is *false*.
* ``host`` - The host the hub should be run on. Default is *'localhost'*
* ``port`` - The port the hub should be run on. Default is *4444*.

## vaadinTestbenchNode

### Configurations
* ``enabled`` - Should the node be enabled. Default is *false*.
* ``host`` - The hostname of the node. Default is *'localhost'*
* ``port`` - The port of the node. Default is *4445*.
* ``hub`` - The hub to connect to. Default is *http://localhost:4444/grid/register*.
* ``browsers`` - TA list of browser configurations. e.g. ``browsers = [[ browserName: 'firefox', version: 3.6, 
maxInstances: 5, platform: 'LINUX' ],...]``. See http://code.google.com/p/selenium/wiki/Grid2 for more information about available browsers and settings. 
The browser setting will be stringified into the -browser parameter for the hub.

## vaadinAddonZip

Create Vaadin Directory compatible Addon zip archive of the project. Metadata can be configurated with the vaadin.addon.* properties

## vaadinJavadocJar

Generate javadoc from project and package it as a jar.

## vaadinSourcesJar
 
Packages all sources a jar.

## vaadinClassPathJar

Builds a classpath jar that is used for operating systems with limited command lengths (Windows).

## vaadinUpdateAddonStyles

Updates the addon.scss file listing with addons styles found in the classpath.

## vaadinUpdateWidgetset

Updates the widgetset (gwt.xml) file with inherits found from the project classpath.