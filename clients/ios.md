# iOS guide

## Setup

On your backend, add an iOS client to your _JCrystalConfig_ file: 

```java
...
public class JCrystalConfig {
	public static void config(){
		...
		CLIENT.addiOS("iOS")  //you can use your custom id
			.setOutput("../iOSProject")  //Point this to your iOS src folder
			.setServerUrl("https://yourserver.com/");
        ...
	}
}
```

After you write this configuration and run jCrystal, on your backend you will have a new annotation available: `@@ClientIOS` which you can use to annotate the web services that will be used by the iOS client.

Tip: You can have multiple iOS clients for a project, all you have to do is add them with different ids and an annotation `@Client<your id>` will be generated.

Add to your iOS project:
- The framework `jCrystaliOSLib.framework`.
- The files of the jCrystal generated folder.

Important: As of now, you have to remove the reference to the jCrystal folder from your project and add it again to see the new files. 

## Web Services
Whenever you want a WS to be used by your iOS client, you only have to annotate it with the iOS generated annotation on your backend:

```java
package company.example.controllers;

public class ManagerHello {

	@ClientIOS
	public static String ping(){
		return "Pong";
	}
}
```

After you define a method, class or package annotated with the generated iOS annotation and run jCrystal, code will be generated and you will have to add the new files to your iOS project. Then you can call your web services in the following way:

```swift
    ManagerHello.ping(onSuccess: { (resp) in
        //On success
    }) { (error) in
        //On error
    }
```

jCrystal can manage the error handling on a UIViewController, showing an alert with the error message if a web service returns an error. Therefore, if you want jCrystal to manage errors, you don't have to implement the error handler:


```swift
class MyViewController: UIViewController {
...
    ManagerHello.ping(onSuccess: { (resp) in
        //On success
    })
...
}
```

## Additional Utilities

- Scroll utilities.
- Form utilities.