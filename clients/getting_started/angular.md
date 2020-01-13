# Hello world on Angular

## Before you begin
Please make sure you have created a jCrystal project. If you don't have a jCrystal project, please follow [our guide to create a new project](creating_project.md).

## Working with an Angular client
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


## Setting up your Angular application

As was explained earlier, you can:

- [Create a new Angular application and set it up to use jCrystal.](#create-a-new-angular-application)
- [Setup an already created Angular application.](#set-up-an-already-created-angular-application)

### Create a new Angular application 

To follow this guide you must have the Angular local environment ready. You can find help on that regard on [this angular page](https://angular.io/guide/setup-local).

Follow these steps to create a new Angular application:

1. Run this command:

    ```
    ng new my-angular-app
    ```

2. This command will ask you about the features of your app, you can choose the default ones by pressing **Enter**. 

3. Go to the folder of you app:

    ```
    cd my-angular-app
    ```

### Set up an already created Angular application

Follow these steps to set up an already created Angular application to support jCrystal:

1. Go to the folder of your app and add the following dependencies using `npm`:
    ```
    npm install moment --save
    npm install sweetalert2 --save
    ```
    If you use a different package manager, please check how to add these dependencies on these websites: 
    - [moment.js](https://momentjs.com/)
    - [sweetalert2](https://github.com/sweetalert2/sweetalert2)

2. On your Angular project add an AppConfiguration class on `src/app/utils/app-configuration.ts`:
    ```typescript
    export class AppConfiguration {
        static DEBUG = true;
    }
    ```

3. On the _app.module.ts_ file of your Angular project add `HttpClientModule` to your imports:

    ```typescript
    import { HttpClientModule } from '@angular/common/http';
    ...
    @NgModule({
        ...
        imports: [
            ...
            HttpClientModule,
        ],
        ...
    })
    export class AppModule { }
    ```

You are ready to use jCrystal on your Angular application! :tada:

## Adding and using a client in your jCrystal project
Now that your Angular application is ready to use jCrystal, we are going to go back to your **jCrystal project** on Eclipse. 

Why? Because we need to tell your backend jCrystal project that it has a front-end project or **client** related. jCrystal supports multiple platforms and each project of a platform is what we call a **client**. 

### Adding a client in your jCrystal project
Follow the next steps to add your Angular application as a client to your jCrystal project:

1. Open the file `jCrystalConfig.java` on `src/main/java`.

2. In the `config()` method, uncomment the line:

    ```java
    addAngularExample();
    ```

    Your `config()` method should look like this:

    ```java
    public class JCrystalConfig {
        ...
        public static void config(){
            //SERVER.firebaseKey = "your firebase key file.json";//It must be placed on WEB-INF
            
            addAngularExample();
            //addAndroidExample();
            //addSwiftiOSExample();
            //addMobileExample();
            //addFlutterExample();
        }
    }
    ```
3. Go to the `addAngularExample()` method. It should look like this:

    ```java
	private static void addAngularExample(){
		CLIENT.add(ClientType.TYPESCRIPT, "web")
			.setOutput("./angulargeneratedcode")
			.setServerUrl(TEST_SERVER_URL);
			//.setServerUrl(PROD_SERVER_URL);
	}
    ```

4. On the `addAngularExample()` method, change this string `"./angulargeneratedcode"` with the path of your Angular application in your computer followed by `src/app`. 
    
    Your method should now look like this:

    ```java
	private static void addAngularExample(){
		CLIENT.add(ClientType.TYPESCRIPT, "web") //1
			.setOutput("<AngularAppPath>/src/app") //2
			.setServerUrl(TEST_SERVER_URL); //3
			//.setServerUrl(PROD_SERVER_URL);
	}
    ```
    Where `<AngularAppPath>` is path of your Angular application in your computer.

    This is what’s happening on each of the lines of the code above:

    - On the line 1, we are adding a Client, whose type is `TYPESCRIPT` and we are setting its id as `web`. The id helps us to identify a client.

    - On the line 2, we are telling jCrystal were it must put the generated code for that client.

    - On the line 3, we are telling jCrystal that server will be hosted on `TEST_SERVER_URL` which, if you check, is `http://localhost:8080/`. We are setting it like this, to test our project locally.

5. Save your changes and run jCrystal by going to your Package Explorer, select your project and: 
    - Pressing `CTRL + 6` (Windows) or `CMD + 6` (Mac OS).

        or
    - Pressing the jCrystal icon. <img src="../images/logo_min.png" alt="jCrystal Logo">

    Why is this necessary? Because jCrystal is going to create an annotation for your client, so you can annotate the web services that are going to be used by that client. We'll see it in the next section :wink:.

### Creating a webservice
Follow the next steps to add a web service and tell jCrystal that your Angular client is going to use it:

1. Check if you have a package named `controllers` on your Eclipse project. If you don't have it, create a package named `controllers`.
2. Create a new java class inside the `controllers` package named `ManagerHelloAngular.java`.
3. Paste this inside that class:

    ```java
    package controllers;
    import jcrystal.clients.ClientWeb;

    public class ManagerHelloAngular {

        @ClientWeb
        public static String helloWorldAngular(){
            return "Hello World to Angular from jCrystal!";
        }
    }
    ```

    Please notice the `@ClientWeb` annotation that indicates that the web service `helloWorldAngular` is going to be used by the client with the id "web".

    **Pro Tip:** Check out what happens if you change the id of your client on the `jCrystalConfig` file from "web" to "angular", and you run jCrystal again. 
    The "@ClientWeb" annotation will disappear :open_mouth: and you will find a new "@ClientAngular" annotation! Cool, right? :grin:

4. Save your changes and run jCrystal by going to your Package Explorer, select your project and: 
    - Pressing `CTRL + 6` (Windows) or `CMD + 6` (Mac OS).

        or
    - Pressing the jCrystal icon. <img src="../images/logo_min.png" alt="jCrystal Logo">
    
5. Run your server by clicking on your project and selecting `Run As > App Engine`. 

We have completed everything required on the jCrystal project side to use the web service on the Angular application. 

## Using the jCrystal service on your Angular application

Let's go back to your Angular application. Follow the next steps to use the jCrystal service on your Angular application:

1. Check on your Angular application project that a new folder was created called `jcrystal` on the folder `src/app`. 

    If you don't see this folder, please go back to Eclipse, make sure that all your files are **saved** and run jCrystal once again.

2. To use your web service on any component you have only have to add `HttpClient` to the constructor of your component:
    ```typescript
    ...
    import { HttpClient } from '@angular/common/http';
    export class MyComponent {
        constructor(public http: HttpClient) { }
    }
    ```

3. To use your service, only call it from a class named `ManagerHelloAngular`, like this:

    ```typescript
    ...
    import { HttpClient } from '@angular/common/http';
    import { ManagerHelloAngular } from './jcrystal/services/ManagerHelloAngular';

    export class MyComponent {
        constructor(public http: HttpClient) { }
        ...
        ManagerHelloAngular.helloWorldAngular(this, resp => {
            alert(resp); //On success
        }, error => {
            alert('An error happened' + error.mensaje); //On error
        });
        ...
    }
    ```

    What did just happened? Why are you seeing a class named exactly like the class that you created on your **backend**?
 
    That's all thanks to jCrystal! jCrystal generated for you everything you need to consume your service `helloWorldAngular` in a straight forward way! You just have to call a method and implement what happens if your request is successful or if and error happens. 

    
## Test

Let's test that your Angular application communicates with your server:

1. Check that your server is running by going to a browser to http://localhost:8080/api/helloAngular/helloWorldAngular. You should see something like:

    ```json
    {"success":1,"r":"Hello World to Angular from jCrystal!"}
    ```

    If not, please go to Eclipse, click on your project and select `Run As > App Engine`.
    
2. On your Angular application, open the file `app.component.html` and put these lines of code:

    ```html
     <button (click)="onClick()">Test jCrystal</button>
    ```

    If you want, replace everything that's in the `app.component.html` with these lines of code. If not, make sure that the button is placed somewhere that you can easily click.

3. Open the file `app.component.ts` and add `HttpClient` to the constructor:
    ```typescript
    ...
    import { HttpClient } from '@angular/common/http';
    export class AppComponent {
        ...
        constructor(public http: HttpClient) { }
    }
    ```

4. Add this method to the `app.component.ts` class:
    ```typescript
    ...
    import { ManagerHelloAngular } from './jcrystal/services/ManagerHelloAngular';
    import { HttpClient } from '@angular/common/http';
    export class AppComponent {
        ...
        constructor(public http: HttpClient) { }
        ...
        onClick() {
            ManagerHelloAngular.helloWorldAngular(this, resp => {
                alert(resp);
            }, error => {
                alert('An error happened' + error.mensaje);
            });
        }
        ...
    }
    ```

5. Run your Angular application:
    ```
    ng serve
    ```

6. Go to http://localhost:4200/ and click the button that says "Test jCrystal".

     After a while, you should see an alert popping up with the message "Hello World to Angular from jCrystal!".

Hurray! :tada: You have created a web service on your backend and have used it on your frontend!

To do this, you didn't have to worry about:

- Parsing the answer from the server.
- Doing http calls on your front end for the web service that you created on your backend.

With jCrystal you will never have to worry about this things. :wink:

Also, from now on, if you want to create a service that it's used by your Angular application you just have to:

1. Define the method of the service on your jCrystal project (Eclipse).
2. Annotate the method with `@ClientWeb`.
3. Run jCrystal.
4. Call that method on your front end and implement what to do if the request is successful or failed.


## What's next
- [Learn more about adding clients to your app](../../clients/general.md).
- [Learn more about web services](../../server/webservices.md).
