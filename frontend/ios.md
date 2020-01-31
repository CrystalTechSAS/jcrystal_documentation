# iOS guide

## Setup

### Backend
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

After you write this configuration and run jCrystal, on your backend you will have a new annotation available: `@ClientIOS` which you can use to annotate the web services that will be used by the iOS client.

Tip: You can have multiple iOS clients for a project, all you have to do is add them with different ids and an annotation `@Client<your id>` will be generated.

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

Remember to Run jCrystal to generate the client files. 

### iOS project
Please do this setup **after** you have created the `@ClientiOS` annotation, annotated a method with it and have successfully run jCrystal.

1. Open your iOS project on Xcode.
2. Right-click on your project and select "Add files to <Your Project Name>...".
3. On the dialog:
	1. Search and select the jCrystal folder which should be on the root folder of your project. 
	2. Select the option "Create folder references".
	3. Click **Add**.
4. Go to your project's target general settings and on the "Frameworks, Libraries and Embedded Content" section click "+".

<img src="../images/ios_frameworks.png" alt="Frameworks">

5. On the dialog, select jCrystal and click **Add**. 
<img src="../images/ios_jcrystal.png" alt="Add dialog">

Now you can integrate with your backend. 

## Web Services

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