# Create project key

To use jCrystal you need add a key to your project. To get the key:

1. Sign in or register in jCrystal:
    - [Sign in](https://jcrystal.dev/#/index/login)
    - [Register](https://jcrystal.dev/#/index/registry)
2. Create a new project with the name of your project.
3. Copy the project key.
4. Go to Eclipse, right-click your jCrystal project and select `jCrystal> Dev key`.
5. Paste the key in the dialog an click on the "Ok" button.

# Test

To test that everything is working as expected:
1. Create a new package named `controllers` on your Eclipse project.
2. Create a new java class inside the `controllers` package named `ManagerHello.java`.
3. Paste this inside that class:

```java
...
public class ManagerHello {
	public static String helloworld(){
		return "Hello World from jCrystal!";
	}
}
```
4. Run jCrystal by going to your Package Explorer, select your project and: 
    - Pressing `CTRL + 6` (Windows) or `CMD + 6` (Mac OS).

        or
    - Pressing the jCrystal icon. ![jCrystal Logo](https://github.com/CrystalTechSAS/jcrystal_documentation/raw/master/images/logo_min.png "jCrystal Logo")
    
5. Refresh your project (`F5`).
6. Run your server by clicking on your project and selecting `Run As > App Engine`.
7. Go to _http://localhost:8080/api/hello/helloworld_ you should see this:
```json
{"success":1,"r":"Hello World from jCrystal!"}
```

Congratulations! You have created your first web service! Easy, right? :)

You are ready to start building! Let's create something amazing! 

## What's next
- [jCrystal Paradigm](paradigm.md).
- [Learn more about web services](../server/webservices.md).
- [Add a client to your app](../clients/general.md).
