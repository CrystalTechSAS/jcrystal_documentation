# General Clients guide

This guide will explain the general concepts of configuring and using clients in a jCrystal project. Please check the respective platform guides for specific information related to them:

- [Android](../clients/android.md)
- [iOS](../clients/ios.md)
- [Angular 7](../clients/angular7.md)
- [jQuery](../clients/jQuery.md)
- Flutter //TODO
- Console //TODO
- Java //TODO

## Setup
jCrystal supports multiple platforms and multiple clients for each of them. A client is defined by a platform (Android, iOS, Mobile, Angular, jQuery, Flutter) and a custom client identifier. 

To add a client, you must add it in your _JCrystalConfig_ file: 

```java
...
public class JCrystalConfig {
	public static void config(){
		...
		CLIENT.add(<type>, <id>)
			.setOutput("../src")  //Point this to your client src project (see each platform)
			.setServerUrl("https://yourserver.com/");
        ...
	}
}
```

Where `<type>` is a `ClientType` and can be:

- `ClientType.TYPESCRIPT`
- `ClientType.JQUERY`

And `<id>` is any unique string that identifies your client.

To add an Android and iOS clients there are special methods:

```java
...
public class JCrystalConfig {
	public static void config(){
		...
        //Add an android client
		CLIENT.addAndroid(<androidId>)  //you can use your custom id
			//.enableFirebasCrashReporting()
			.setOutput("../AndroidApp/app/src/main/java")  //Point this to your android project src folder
			.setServerUrl("https://yourserver.com/");
        //Add an iOS client
 		CLIENT.addiOS(<iOSId>)  //you can use your custom id
			.setOutput("../iOSProject")  //Point this to your iOS src folder
			.setServerUrl("https://yourserver.com/");
        ...       
	}
}
```

After you write this configuration and run jCrystal, you will have on your backend a new annotation available: `@Client<id>` where `<id>` is the custom identifier you set for the client. You can use this annotation to mark the web services that will be used by your client. In this way, you differentiate which client access which services. 
Please notice that until you use your annotation no code will be generated for your client. 

Sometimes both iOS and Android apps have the same functionality and therefore consume the same web services. In that case, you can add a mobile client that will manage both platforms:


```java
...
public class JCrystalConfig {
	public static void config(){
		...
        //Add an android client
		CLIENT.addMobile(<id>)
		    .setOutputAndroid("../AndroidApp/app/src/main/java")  //Point this to your android project src folder
		    .setOutputiOS("../iOSProject")  //Point this to your iOS src folder
		    .setServerUrl("https://yourserver.com/");
	}
}
```

Important: This is only the backend setup, to know what you have to do to setup each platform project, please check the respective platform guides.

## Web services
Whenever you want a web service to be used by your specific client, you only have to annotate it with the generated annotation on your backend. 

As an example, let's assume we have defined this client:

```java
...
public class JCrystalConfig {
	public static void config(){
		...
		CLIENT.add(ClientType.TYPESCRIPT, "web")
			.setOutput("../AngularApp/src/app")
			.setServerUrl("https://yourserver.com/");
        ...
	}
}
```
After running jCrystal you will have an `@ClientWeb` annotation available that you can use in this way:

### Annotate web services

```java
package company.example.controllers;

public class ManagerHello {

	@ClientWeb
	public static String ping(){
		return "Pong";
	}
}
```

By writing this and running jCrystal once again, jCrystal will generate the code to consume the `ping` service on your Angular project, specifically in the folder `../AngularApp/src/app/jcrystal`. If you want to know how to consume this service from the client-side, check the platform guide.

### Annotate classes

Sometimes, you have a very long class with services and all of them are used by the same client. In such case, you can annotate the whole class and jCrystal will understand that all the web services inside that class are used by that client:

```java
package company.example.controllers;
@ClientWeb
public class ManagerHello {
	public static String ping(){
		return "Pong";
	}
    ...
    public static String hello(){
		return "Hi from jCrystal!";
	}
}
```

By writing this and running jCrystal once again, jCrystal will generate the code to consume all the web services declared on `ManagerHello` on your Angular project.

### Annotate packages

Likewise, is possible to annotate a whole package inside your project to mark that all the web services defined inside all the classes of that package will be used by a client. You can do this by creating a new class inside that package named `package-info.java` with these contents:

```java
@jcrystal.clients.ClientWeb
package company.example.controllers; //The package.
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
jCrystal uses a custom token session management by configuring a `<TokenEntity>` (where `<TokenEntity>` is name such as `Token`) entity that will manage the session token. Whenever such configuration is made that entity will be generated on the client side with the usual methods of generated entities but also methods related to the user authentication:

- `store<TokenEntity>()`: Method to store and cache in your local database this entity.
- `get<TokenEntity>()`: Method to get from your cache or your local database this entity.
- `delete<TokenEntity>()`: Method to delete the entity of the local database and cache.
- `isAuthenticated()`: Method to know if the user is authenticated in the app.

jCrystal automatically saves and sends the token from the client side whenever the token is received from the server or required by it to consume a web service. Therefore, as a developer your responsibility related with the authentication will be to check if the user is authenticated to show him the appropriate information and delete the `<TokenEntity>` from the local database whenever the user logs out of the system. 

### Utilities

There are several entity utilites that can help to manage arrays of given entity: 

- Sort
- MapList
- Group