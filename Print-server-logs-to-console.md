By default the plugin will write the server logs to build/jetty/. However when developing an application it would useful to see what is happening with the server in real time from the console instead of having to open up the log file. To do that you need to provide the following option in your build configuration:

```
vaadin {
    plugin {
        logToConsole true
    }
}
```