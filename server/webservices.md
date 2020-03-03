# Web Services

## Overview
jCrystal is designed to easily create, expose and consume RESTful web services. Moreover, one of our main goals is to speed up the development of multiplatform applications, so we have a strong focus on Web APIs development, as such:

- There is currently no support for server-side views or features typical of a traditional server-side MVC framework.
- We only support JSON responses, except for the web services that upload/download files. 

What does this mean for you? This only means that when developing your backend you only have to focus on creating web services and entities; meanwhile, your clients (web, mobile, etc) will easily consume those web services thanks to the code generated from jCrystal. 

## Basics

In jCrystal, a web service is one **method**, as simple as this:

```java
package company.example.controllers;

public class ManagerTest {
	public static String helloworld(){
		return "Hello world from jCrystal!";
	}
}
```
This method generates a GET web service:
- It doesn't receive any query parameters, **just like the method** that defines it.
- It returns a JSON with the text "Hello world from jCrystal!", **just like the method** that defines it.
- The web service can be found in `/api/test/helloWorld`, **just like the method** that defines it is in the Manager**Test** class and has **helloWorld** as the name.

As you can see, everything required to completely define your web service is inside this one simple method.

But wait, where did you define the type of the web service and the route? Nowhere! jCrystal is a framework that uses the paradigm "convention over configuration", that's why by convention jCrystal:
- Decides that this web service is an HTTP GET since the parameters don't include a POST entity or a file. 
- Decides that the route is `/api/` plus the name of the class of the method without the word "Manager", in this case, `test/`; plus the name of the method, in this case, `helloWorld`.  So the final route is `/api/test/helloWorld`.

Additionally, to be a web service, the method has to be:
- **public static**.
- Defined on a class with Manager as name prefix.
- The class should be inside a package that at some point has a folder named `controllers`.

Therefore, the following method is also another valid web service:

```java
package company.example.controllers.mobile.test; //The package has one folder named "controllers"

public class ManagerTestHello { //The name of the class starts with "Manager"
	public static String hello(String name) { //The method is public static
		return "Hello, "+ name;
	}
}
```

## Parameters

As explained previously, jCrystal uses each component of a method to define a web service. The **parameters** of the method are the query parameters or the body of the web service. 

The names and types of your parameters will be the same used on the web service and on the code generated to consume this web service, so please choose clear and meaningful parameter names. 

jCrystal supports several parameter types for your web services:

- Native types and native object types (int, Integer, long, Long, boolean, Boolean, double, Double).
- String.
- Enumerations. 
- [CrystalDates*](utils/crystal_dates.md) (Use them instead of any Date class).
- Entities.
- Post types.
- Jsonify data transfer objects.
- Arrays and lists of previous types.

## Responses

- The **value returned** by the method is the response of the web service. The type of the returned value is the same used on the code generated to consume this web service. 

A web service can return:

- Native types and native object types (int, Integer, long, Long, boolean, Boolean, double, Double)
- String.
- Enumerations.
- [CrystalDates*](utils/crystal_dates.md) (Use them instead of any Date class).
- Entities.
- Post types.
- Jsonify data transfer objects.
- Arrays and lists of previous types.
- Tuples of previous types.


## Routes
By convention, the **method name**, **name of the class** where the method is defined and the **package where the class** are used to define the route of the web service. 


## Simple examples

## FAQ
Can you override those conventions? Yes, you can! Check the annotations @Path and @PathMethod. However, our suggestion is that you try to use the jCrystal conventions as much as you can since they will speed up your development.

## Complex data upload

## File uploads

```java
public static void A(FileUploadDescriptor desc) throws Exception{
	desc.put("bucket", "nombre.txt");
	
}
```