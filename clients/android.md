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

On your Android project, include the following changes on the module gradle:

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

And the following changes on your rood build.gradle:
```gradle
allprojects {
    repositories {
		....
		maven { url 'https://jitpack.io' }
	}
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
## Entities
jCrystal entities will be generated on the client folder whenever a web service annotated with the generated client annotation receives or returns a jEntity.

One jEntity will generate several related files on the client: 
- One class that has all the attributes, methods to access them and change them as well as helpful utility methods.
- One or more interfaces that specify the access level of the entity. This will help you know what level of detail will be required or received by the web service. 
- One class to manage the local storage of the entity. (Only available on Android and iOS)


### Entity access levels
//TODO: How to use the levels.

### Local Database (Only available on Android and iOS)
Each jEntity generates a file named `DB<jEntityName>` where you can find methods to store, retrieve and delete an entity or array of the entities in the local database. To use these methods the only thing required is to keep a key that will identify the element being stored and will help to store it and delete it. 

// TODO: Part keys. 

### Token Entity
jCrystal uses a custom token session management by configuring a `<TokenEntity>` entity that will manage the session token ([as shown here](../server/auth)). Whenever such configuration is made that entity will be generated on the client side with the usual methods of generated entities but also methods related to the user authentication:

- `store<TokenEntity>()`: Method to store and cache in your local database this entity.
- `get<TokenEntity>()`: Method to get from your cache or your local database this entity.
- `delete<TokenEntity>()`: Method to delete the entity of the local database and cache.
- `isAuthenticated()`: Method to know if the user is authenticated in the app.

jCrystal automatically saves and sends the token from the client side whenever the token is received from the server or required by it to consume a web service. Therefore, as a developer your responsibility related with the authentication will be to check if the user is authenticated to show him the appropriate information and delete the `<TokenEntity>` from the local database whenever the user logs out of the system. 

## Additional Utilities

- Create table and grid views easily
- Layout connection utilites