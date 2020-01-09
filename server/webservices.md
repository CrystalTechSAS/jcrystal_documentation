# jCrystal Web Services

With jCrystal one web service is a method:

```java
package company.example.controllers;

public class Manager {
	public static String helloworld(){
		return "Hello World from jCrystal!";
	}
}
```

To be a WS, a method should be:
- **public**
- Defined on a class with _Manager_ as name prefix.
- The class should be inside a package with the name _controllers_ as one of its parents. 

The following is also a web service:

```java
package company.example.controllers.mobile.test;

public class ManagerHello {
	public static String ping(){
		return "Pong";
	}
}
```

## Parameters

jCrystal supports several parameter types for your WSs:

- Native types and native object types (int, Integer, long, Long, boolean, Boolean, double, Double)
- Strings
- [Entities and post types](webservices_posts.md)
- [Jsonify data transfer objects](webservices_post.md)
- Arrays and lists of previous types
- [Files](webservices_post.md)

## Responses

A WS can return:

- Native types and native object types (int, Integer, long, Long, boolean, Boolean, double, Double)
- Strings
- Entities post types
- Jsonify data transfer objects
- Arrays and lists of previous types
- Tuples

## Simple examples

## Complex data upload

## File uploads

```java
public static void A(FileUploadDescriptor desc) throws Exception{
	desc.put("bucket", "nombre.txt");
	
}
```