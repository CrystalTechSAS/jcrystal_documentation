# Setup

## Using Eclipse plugin
You must have Java 1.8+ installed.

1. Install Eclipse IDE for Java EE Developers, version 4.7 or later: [Eclipse](http://www.eclipse.org/downloads/eclipse-packages/). 
2. Install [Google Cloud Plugin](https://cloud.google.com/eclipse/docs/quickstart).
3. Install Eclipse jCrystal Plugin: 

    1. On MacOS select `Help > Install New Software...`

    2. Click the "Add" button.

    3. On the new dialog, set the name as "jCrystal" and the "Location" as 
 _https://www.jcrystal.dev/plugin/_

    4. Click the "Add" button.

    5. The "Install" dialog should have updated, check de "Tools" checkbox and click on the "Next" button.

    6. Click on the "Next" button.

    7. Choose "I accept the terms of the license agreement" and click "Finish".

    8. Click "Install anyway" if a Security Warning dialog appears.

    9. Restart Eclipse when prompted.

4. Create a new Google App Engine Standard Java Project. Check the "Create as Maven Project" mark on the setup process. 
5. Right-click your new project, go to _jCrystal_ menu and select _Add dependencies_. 
6. On the same parent directory of your _src_ folder, there will be a _utils_ folder that you must add to your build by right-clicking that folder and selecting `Build path > Use as Source Folder`. In this folder will reside generated code for your server.

7. Refresh your project by going to `File > Refresh`.
9. _Optional:_ If it was generated, delete the `Hello App Engine.java` as well as the tests folder. From now on you won't need that much code to create a web service ;). 
8. _Optional:_ If you see any errors, try updating your project from maven by right-clicking project and going to `Maven > Update project`.

You are ready to start building! 

## What's next
- [Create a project key](key.md)

- [Learn how to add your first web service](../server/webservices.md).
- [Add a new client to your app](../clients/general.md).


