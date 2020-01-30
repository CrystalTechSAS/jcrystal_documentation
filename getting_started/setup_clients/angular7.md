# Angular 7 guide

## Setup

Add a typescript client to your _JCrystalConfig_ file: 

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

After you write this configuration and run jCrystal, on your backend you will have a new annotation available: `@ClientWeb` which you can use to annotate the web services that will be used by the Angular client.

On your Angular project add an AppConfiguration class on `src/app/utils/app-configuration.ts`:

```typescript
export class AppConfiguration {
  static DEBUG = true;
}
```

On the _app.module.ts_ file add `HttpClientModule` to your imports:

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

Include the following dependencies using npm:

```
npm install moment --save
npm install sweetalert2 --save
```
If you use a different package manager, please check how to add these dependencies on these websites: 
- [moment.js](https://momentjs.com/)
- [sweetalert2](https://github.com/sweetalert2/sweetalert2)

## Web Services
Whenever you want a WS to be used by your Angular client, you only have to annotate it with the Angular generated annotation on your backend:

```java
package company.example.controllers;

public class ManagerHello {

	@ClientWeb
	public static String ping(){
		return "Pong";
	}
}
```

After you define a method, class or package annotated with the generated Angular annotation and run jCrystal, code will be generated and you will have to add the new files to your Angular project. Then you can call your web services in the following way:

```typescript
...
import { ManagerHello } from './jcrystal/services/ManagerHello';
import { HttpClient } from '@angular/common/http';
export class MyComponent {
	constructor(public http: HttpClient) { }
...
    ManagerHello.ping(this, resp => {
        //On success
    }, error => {
        //On error
    });
...
}
```

Take into account that on your component constructor you must add `public http : HttpClient`. Also remember to import the class of your web service in your component

jCrystal can manage the error handling by showing an alert with the error message if a web service returns an error. Therefore, if you want jCrystal to manage errors, you don't have to implement the error callback:


```typescript
...
import { HttpClient } from '@angular/common/http';
export class MyComponent {
	constructor(public http: HttpClient) { }
...
    ManagerHello.ping(this, resp => {
        //On success
    });
}
```
