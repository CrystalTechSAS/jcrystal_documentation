# Android guide

## Setup

On your backend, add an Android client to your _JCrystalConfig_ file: 

```java
...
public class JCrystalConfig {
	public static void config(){
		...
		CLIENT.addAndroid("android")  //you can use your custom id
			//.enableFirebasCrashReporting()
			.setOutput("../AndroidApp/app/src/main/java")  //Point this to your android project src folder
			.setServerUrl("https://yourserver.com/");
    	...
	}
}
```

After you write this configuration and run jCrystal, on your backend you will have a new annotation available: `@ClientAndroid` which you can use to annotate the web services that will be used by the android client.

Tip: You can have multiple android clients for a project, all you have to do is add them with different ids and an annotation `@Client<your id>` will be generated.


On your Android project, include the following changes on your rood build.gradle:
```gradle
allprojects {
    repositories {
		....
		maven { url 'https://jitpack.io' }
	}
}
```

And the following changes on the module gradle:
```gradle
android {
  ...
  // Configure your module to use Java 8 language features
  compileOptions {
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
  }
}
dependencies {
    ...
    implementation 'com.github.CrystalTechSAS:jCrystalAndroidLib:342e96e77d'
}
```

## Web Services
Whenever you want a WS to be used by your android client, you only have to annotate it with the android generated annotation on your backend:

```java
package company.example.controllers;

public class ManagerHello {

	@ClientAndroid
	public static String ping(){
		return "Pong";
	}
}
```

After you define a method, class or package annotated  with the generated android annotation and run jCrystal, code will be generated and added to your android project. Then you can call your web services in the following way:

```java
import jcrystal.mobile.net.controllers.ManagerHello;
...
    ManagerHello.ping(this, resp -> {
      	//On success
    }, error -> {
		//On error
	});
```

Where `this` can be an `Activity` or `Fragment`.

If you have an activity that calls multiple web services and the error management of those web services is the same (for example, showing a Toast), you can implement `OnErrorListener` on your activity so to avoid rewriting the error callback: 

```java
import jcrystal.mobile.net.controllers.ManagerHello;
import jcrystal.mobile.net.utils.OnErrorListener;
import jcrystal.mobile.net.utils.RequestError;

public class MyActivity extends Activity implements OnErrorListener {
...
    ManagerHello.ping(this, resp -> {
      	//On success
    });

	...

	public void onError(RequestError error) {
		//On error
    }
}
```

## Additional Utilities

- Create table and grid views easily
- Layout connection utilites