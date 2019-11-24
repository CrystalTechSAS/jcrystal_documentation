# Angular 7 guide

## Setup

Add a typescript client to your _JCrystalConfig_ file: 

```java
...
public class JCrystalConfig {
	public static void config(){
		...
		CLIENT.add(ClientType.TYPESCRIPT, "web")  //you can use your custom id
			.setOutput("../angulargeneratedcode") //Point this to you angular project src folder
			.setServerUrl("https://yourserver.com/");
    ...
	}
}
```

Also, add an AppConfiguration class on `src/util/app-configuration.ts` to you angular project:

```typescript
export class AppConfiguration{
  static DEBUG = true;
}
```

Include the following dependencies using npm:

- [moment](https://www.npmjs.com/package/moment)
- [sweetalert](https://www.npmjs.com/package/sweetalert)

## Web Services

Call your web services on the following way:

```typescript
    ManagerHello.ping(this, ()=>{
      	//On success
    }, error=>{
		//On error
	});
```

On your component constructor you must add `public http : HttpClient`.
