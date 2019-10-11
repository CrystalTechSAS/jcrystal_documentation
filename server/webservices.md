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

To be a WS, a method should be public, defined on a class with _Manager_ as name prefix and should be inside a package named _controllers_ as some of its parent. The following is also a web service:

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
- Entities post types
- Jsonify data transfer objects
- Arrays and lists of previous types
- Files

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