# Hello world on Android

## Before you begin
Please make sure you have created a jCrystal project. If you don't have a jCrystal project, please follow [our guide to create a new project](creating_project.md).

## Working with an Android client
jCrystal is a full-stack framework that aims to reduce code rewrites, moreover, on your frontend clients it will help you:

- Access your web services with zero effort.
- Access your objects model with zero effort.

As a front-end developer, this means that:

- You **can use your own code editor for your front-end client**.

    Feel free to use the code editor that you are most familiar with on your client-side. jCrystal is here to make you **faster** (we'll soon see how!), not to force you to change everything you know about front-end development

- You are in charge of creating your front-end project.

    jCrystal will make everything easier for you, but you are still in charge of creating your front-end project. Don't worry, that only means you can customize it as much as you want!

    That also means jCrystal can be used on a front-end project that's already created.

- You are in charge of setting up the project to support jCrystal.

    Don't worry, this usually means adding a couple of dependencies to your front-end project. :wink:


## Setting up your Android application
Follow the next steps to set up your Android application to use jCrystal:

1. On your Android project, your root `build.gradle` and include the following lines:
    ```gradle
    allprojects {
        repositories {
            ....
            maven { url 'https://jitpack.io' }
        }
    }
    ```

2. Open your module `build.gradle` and include these lines:
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
        implementation 'com.github.CrystalTechSAS:jCrystalAndroidLib:b1499a6f2b'
    }
    ```

You are ready to use jCrystal on your Android application! :tada:

## Adding and using a client in your jCrystal project
Now that your Android application is ready to use jCrystal, we are going to go back to your **jCrystal project** on Eclipse. 

Why? Because we need to tell your backend jCrystal project that it has a front-end project or **client** related. jCrystal supports multiple platforms and each project of a platform is what we call a **client**. 

### Adding a client in your jCrystal project
Follow the next steps to add your Android application as a client to your jCrystal project:

1. Open the file `jCrystalConfig.java` on `src/main/java`.

2. In the `config()` method, uncomment the line:

    ```java
    addAndroidExample();
    ```

    Your `config()` method should look like this:

    ```java
    public class JCrystalConfig {
        ...
        public static void config(){
            //SERVER.firebaseKey = "your firebase key file.json";//It must be placed on WEB-INF
            
            //addAngularExample();
            addAndroidExample();
            //addSwiftiOSExample();
            //addMobileExample();
            //addFlutterExample();
        }
    }
    ```
3. Go to the `addAndroidExample()` method. It should look like this:

    ```java
	private static void addAndroidExample(){
		CLIENT.addAndroid("android")
			//.enableFirebasCrashReporting()
			.setOutput("./androidgeneratedcode")
			.setServerUrl(TEST_SERVER_URL);
			//.setServerUrl(PROD_SERVER_URL);
	}
    ```

4. On the `addAndroidExample()` method, change this string `"./androidgeneratedcode"` with the path of your Android application in your computer followed by `/app/src/main/java`. 
    
    Your method should now look like this:

    ```java
	private static void addAndroidExample(){
		CLIENT.addAndroid("android") // 1 
			//.enableFirebasCrashReporting() 
			.setOutput("<AndroidAppPath>/app/src/main/java") // 2
			.setServerUrl(TEST_SERVER_URL); // 3
			//.setServerUrl(PROD_SERVER_URL);
	}
    ```
    Where `<AndroidAppPath>` is the path of your Android application in your computer.

    This is what’s happening on each of the lines of the code above:

    - On the line 1, we are adding an Android client and we are setting its id as `android`. The id helps us to identify a client. This allows you to have multiple android application using different services of the backend. 

    - On the line 2, we are telling jCrystal were it must put the generated code for that client.

    - On the line 3, we are telling jCrystal that server will be hosted on `TEST_SERVER_URL` which, if you check, is `http://localhost:8080/`. We are setting it like this, to test our project locally.

5. Save your changes and run jCrystal by going to your Package Explorer, select your project and: 
    - Pressing `CTRL + 6` (Windows) or `CMD + 6` (Mac OS).

        or
    - Pressing the jCrystal icon. <img src="../../images/logo_min.png" alt="jCrystal Logo">

    Why is this necessary? Because jCrystal is going to create an annotation for your client, so you can annotate the web services that are going to be used by that client. We'll see it in the next section :wink:.

### Creating a webservice
Follow the next steps to add a web service and tell jCrystal that your Android client is going to use it:

1. Check if you have a package named `controllers` on your Eclipse project. If you don't have it, create a package named `controllers`.
2. Create a new java class inside the `controllers` package named `ManagerHelloAndroid.java`.
3. Paste this inside that class:

    ```java
    package controllers;
    import jcrystal.clients.ClientWeb;

    public class ManagerHelloAndroid {

        @ClientAndroid
        public static String helloWorldAndroid(){
            return "Hello World to Android from jCrystal!";
        }
    }
    ```

    Please notice the `@ClientAndroid` annotation that indicates that the web service `helloWorldAndroid` is going to be used by the client with the id "web".

    **Pro Tip:** Check out what happens if you change the id of your client on the `jCrystalConfig` file from "android" to "app", and you run jCrystal again. 
    The "@ClientAndroid" annotation will disappear :open_mouth: and you will find a new "@ClientApp" annotation! Cool, right? :grin:

4. Save your changes and run jCrystal by going to your Package Explorer, select your project and: 
    - Pressing `CTRL + 6` (Windows) or `CMD + 6` (Mac OS).

        or
    - Pressing the jCrystal icon. <img src="../../images/logo_min.png" alt="jCrystal Logo">
    
5. Run your server by clicking on your project and selecting `Run As > App Engine`. 

We have completed everything required on the jCrystal project side to use the web service on the Android application. 

## Using the jCrystal service on your Android application

Let's go back to your Android application. Follow the next steps to use the jCrystal service on your Android application:

1. Check on your Android application project that a new package was created: `jcrystal.mobile.net` on the folder `app/src/main/java`. 

    If you don't see this folder, please go back to Eclipse, make sure that all your files are **saved** and run jCrystal once again.

2. To use your web service, only call it from a class named `ManagerHelloAndroid`, like this:

    ```java
    import jcrystal.mobile.net.controllers.ManagerHelloAndroid;
    ...
        ManagerHelloAndroid.helloWorldAndroid(this, resp -> {
            //On success
        }, error -> {
            //On error
        });
    ```

    What did just happened? Why are you seeing a class named exactly like the class that you created on your **backend**?
 
    That's all thanks to jCrystal! jCrystal generated for you everything you need to consume your service `helloWorldAndroid` in a straight forward way! You just have to call a method and implement what happens if your request is successful or if an error happens. 


Hurray! :tada: You have created a web service on your backend and know how to use it on your frontend!

Take into account that to consume your web service, you didn't have to worry about:

- Parsing the answer from the server.
- Doing http calls on your front end for the web service that you created on your backend.

With jCrystal you will never have to worry about this things. :wink:

Also, from now on, if you want to create a service that it's used by your Android application you just have to:

1. Define the method of the service on your jCrystal project (Eclipse).
2. Annotate the method with `@ClientAndroid`.
3. Run jCrystal.
4. Call that method on your front end and implement what to do if the request is successful or failed.


## What's next
- [Learn more about adding clients to your app](../../clients/general.md).
- [Learn more about web services](../../server/webservices.md).
