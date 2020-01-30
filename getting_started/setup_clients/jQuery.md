# jQuery guide

## Setup

On your backend, add a jQuery client to your _JCrystalConfig_ file: 

```java
...
public class JCrystalConfig {
	public static void config(){
		...
		CLIENT.add(ClientType.jQuery, "jQuery")  //you can use your custom id
			.setOutput("../jQueryApp/") //Point this to your project src folder
			.setServerUrl("https://yourserver.com/");
    	...
	}
}
```

After you write this configuration and run jCrystal, on your backend you will have a new annotation available: `@ClientJquery` which you can use to annotate the web services that will be used by the jQuery client.

## Web Services
Whenever you want a WS to be used by your jQuery client, you only have to annotate it with the Angular generated annotation on your backend:

```java
package company.example.controllers;

public class ManagerHello {

	@ClientJQuery
	public static String ping(){
		return "Pong";
	}
}
```

After you define a method, class or package annotated with the generated Angular annotation and run jCrystal, jCrystal will generated the file `controller.js` which contains all the logic required to consume your backend webservices like this:


```javascript
...
    ManagerHello.ping(function (resp){
        //On success
    }, function (error) {
        //On error
    });
```