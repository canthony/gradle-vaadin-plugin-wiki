## Using CDI/EJB with your Vaadin project

Vaadin fully supports using CDI. To do that Vaadin provides support via a separate addon you can find in the Vaadin directory (https://vaadin.com/directory#!addon/vaadin-cdi). The Gradle plugin also supports using it out-of-the box with *vaadinRun*.

To use CDI with your application start by including the cdi dependency in your project 

```gradle
dependencies {
	compile 'com.vaadin:vaadin-cdi:1.0.3'
}
```

Once you have added the dependency to your *build.gradle* right click on your project in Eclipse and select *Gradle -> Refresh Gradle Project*. This will download and add the helper classes to your project.


## Injecting your UI
Next, we can **remove any servlet class** the plugin has created. With CDI we will not need any servlet, instead we are going inject the UI's using a annotation provided by the CDI addon.

Now open up your UI class and annotate your UI with the **@CDIUI("")** annotation. This will map your UI with the root context path. If you want to use another context path, for example "/app" you should annotate your UI with **@CDIUI("app")**.


## Injecting services 

To inject services we will need the **@Inject** annotation. This does not come with the addon, instead you should add the following dependency to your *build.gradle*:

```gradle
dependencies {
	compile 'javax.inject:javax.inject:1'
}
```

Once you have added the dependency to your *build.gradle* right click on your project in Eclipse and select *Gradle -> Refresh Gradle Project*. This will download and add the annotation to your project.

Now you can in your UI class for example say

```java
@Inject
private MyService service;
```

And in your service will automatically be injected to the field and you don't have to initiate it with *new Myservice(...)*.

## Example

Here is a full example of an UI you can run with *vaadinRun* and try out.

```java
@Theme("Test")
@CDIUI("")
public class TestUI extends UI{
	
	/*
	 * Injected service
	 */
	@Inject
	private MyService service;
	
	@Override
	protected void init(VaadinRequest request){
		Label lbl = new Label(service.getMessage());
		setContent(lbl);
	}
	
	/*
	 * Service interface
	 */
	public interface MyService {
		
		String getMessage();
	}
	
	/*
	 * Service implementation
	 */
	public static class MyServiceImpl implements MyService {

		@Override
		public String getMessage() {			
			return "Hello vaadin from MyService!";
		}
	}
}
```