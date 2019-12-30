# Creating a new application

## Before you begin

Please make sure you have followed the instructions detailed on [Installation](installation.md).

## Creating a new application project

1. Open Eclipse.

2. Create a new "Google App Engine Standard Java Project". 

3. On the setup dialog:
    - Enter a Project Name 
    - Check the "Create as Maven Project" option.
    - Enter a Group ID and Artifact ID.

4. Click **Finish**. 

5. Right-click your new project, select `jCrystal > Add dependencies`. 

6. Refresh your project by going to `File > Refresh`.

7. Select the `src/main/utils` folder and add it to your build by right-clicking it and selecting `Build path > Use as Source Folder`. This folder will contain the generated code of your server.
    <img src="images/utils_folder.png" alt="Utils folder" height="250">

8.  If you see any errors, try updating your project from maven by right-clicking project and going to `Maven > Update project`.

### Optional steps

These steps are not mandatory, but can help you enjoy your experience with jCrystal:

1. Right click your project and select `Properties`. On the properties dialog, go to `Java Compiler` and check the option "Store information about method parameters". 
     <img src="images/store_information.png" alt="Store information about method parameters" height="700">
2. Click **Apply and Close**. 

3. On the dialog to rebuild the project, click **Yes**.

4. Delete the `Hello App Engine.java` as well as the **`src/java/tests`** folder. From now on you won't need that much code to create a web service :wink:. 


## Create and setup a key

To use jCrystal you need add a key to your project. To get the key:

1. Sign in or register in jCrystal:
    - [Sign in](https://jcrystal.dev/#/index/login)
    - [Register](https://jcrystal.dev/#/index/registry)

2. Create a new project with the name of your project.

3. Copy the project key.

4. Go to Eclipse, right-click your jCrystal project and select `jCrystal > Dev key`.

5. Paste the key in the dialog an click on the "Ok" button.

## Verifying
Your project is ready to be used! :tada: To verify that jCrystal is working:

1. Go to your Package Explorer, select your project and: 
- Pressing  `CTRL + 6` (Windows) or `CMD + 6` (Mac OS).

    or
- Pressing the jCrystal icon. ![jCrystal Logo](https://github.com/CrystalTechSAS/jcrystal_documentation/raw/master/images/logo_min.png "jCrystal Logo")

2. Open the console view by going to `Window > Show View > Console` you should see something like:

```
UTF-8
Time sending (11): 147 ms
Total time: 804 ms
```

So, what did just happened? jCrystal scanned all your project files to know which code to generate to help you develop your app. 

Refresh and check your project, do you see anything different? 

You will find that your project is the same after running jCrystal: nothing was generated. Why is that? That's because your application is still empty, so jCrystal didn't find anything that could generate that would be useful. Go to the next section to [learn how to run your application and really use jCrystal](run_test.md).


## What's next
- [Learn how to run and test your application](run_test.md) 
- Did you encounter an error creating the app? Check our [troubleshooting](troubleshooting.md). 
- [Anatomy of a jCrystal application](anatomy.md) 