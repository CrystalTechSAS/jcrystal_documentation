# Working with a frontend team on jCrystal

Working with a frontend team using jCrystal is really simple. The important thing to remember is that the backend **generates all the integrations and data models for each frontend**, so it's important to ensure a way in which everyone in the team has the updated version of the generated code. 

In our experience, the best way to successfully work with a frontend team is to have the frontend projects under a **version control system** and give write access to those projects to the team in charge of the back-end. In this way, whenever a change is made on the back-end, the **back-end team can generate the frontend client SDKs to each frontend project and commit the change** so that everyone has the updated version of the code. 

Please take into account that there are many ways to implement this: 
- Both the frontend and back-end can be on the same versioned project.
- All the frontends are in one versioned project and the backend is in another.
- Every project (each frontend and the back-end) is in his own versioned project. 
- etc.

All of these alternatives can work! The important thing to keep in mind is to always make a commit and push on every project whenever a change is made on the back-end.

The process to work on a back-end considering there is another team working on the frontend is the following:

1. Fetch all the repositories of the frontend projects on your local PC.
2. Setup on your ``jCrystalConfig.java`` each client for the frontend projects, where the output is set to the repository folder of each frontend. Examples:
    Angular
    ```java
    ...
    public class JCrystalConfig {
        public static void config(){
            ...
            CLIENT.add(ClientType.TYPESCRIPT, "web")  //you can use your custom id
                .setOutput("../AngularApp/src/app") //Point this to your angular project src folder
                .setServerUrl("https://yourserver.com/");
            ...
        }
    }
    ```
    Android
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

    iOS
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


3. Run jCrystal to create each client annotation. After this step, you will have an annotation for each client that you added on  ``jCrystalConfig.java``, like ``@ClientWeb``.

4. Create web services on your back-end and annotate them with your client's annotation whenever that client uses that service.

5. Run jCrystal to generate the client's SDK code.
6. Commit your changes to the repositories of the frontend projects.
7. Repeat step 4.

## Server URL

Another important thing to remember, is that the backend must update the server URL to your production URL whenever you have deployed your backend and your frontend team cannot access localhost.

You can do this on your jCrystalConfig.java file on each client that has been added, like this:

```java
...
public class JCrystalConfig {
    public static void config(){
        ...
        CLIENT.add(ClientType.TYPESCRIPT, "web")
            .setOutput("../AngularApp/src/app")
            .setServerUrl("http://newserver.com/"); //Set the URL of your server
        ...
    }
}
```

Then, run jCrystal once again so that the generated SDK clients have the updated URL and don't forget to update the code of your front-end team.