# Android guide

## Setup

Add an Android client to your _JCrystalConfig_ file: 

```java
...
public class JCrystalConfig {
	public static void config(){
		...
		CLIENT.addAndroid("android")  //you can use your custom id
			//.enableFirebasCrashReporting()
			.setOutput("../androidgeneratedcode")  //Point this to you angular project src folder
			.setServerUrl("https://yourserver.com/");
    ...
	}
}
```

Include the following dependencies on your gradle:


## Web Services

Call your web services on the following way:

```java
    ManagerHello.ping(this, ()=>{
      	//On success
    }, error=>{
		//On error
	});
```