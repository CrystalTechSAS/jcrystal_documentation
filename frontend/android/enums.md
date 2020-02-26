# Enumerations

jCrystal generates the .java files of the enumerations required to communicate with the backend, you can find them in the jCrystal generated folder: `jcrystal/entities/enums`. Each enumeration used by the web services generates one class in java with the same attributes that the enumeration has on the backend. 

All the values of an enumeration have at least the attributes `id` and the method `String rawName()`; both of this elements will help you identify each value of the enumeration. Also, by default jCrystal generates the static method `fromId` to help you get an enumeration value from an id (this could be a int or a String). 

This is an example of a generated enumeration:
```java
package jcrystal.mobile.entities.enums;
public enum Rol{
	OWNER(1),
	BACKEND(2),
	CLIENT(3),
	;
	public final int id;
	Rol(int id){
		this.id = id;
	}
	public String rawName(){
		switch(this){
			case OWNER : return "OWNER";
			case BACKEND : return "BACKEND";
			case CLIENT : return "CLIENT";
		}
		return null;
	}
	public static Rol fromId(int id){
		switch(id){
			case 1: return OWNER;
			case 2: return BACKEND;
			case 3: return CLIENT;
		}
		return null;
	}
}
```

As you can see, given an instance of this class, you can access its attributes directly like this:
```java
import jcrystal.mobile.entities.enums.Rol;
...
Rol rol = Rol.CLIENT;
int idRol = rol.id; 
String rawNameRol = rol.rawName();
```
Whenever you use an enum, don't forget to import the class.

Additionally, you can look up a value of the enumeration given an id:
```java
import jcrystal.mobile.entities.enums.Rol;
...
Rol rol = Rol.fromId(2);
```
Please take into account that type of the parameter `id` may change (can be int or String) and depends on how the enumeration is defined on the backend. The best way to know what kind of type this method requires is to check the signature of the method on the generated enumeration class.


Please take into account that not all the enumerations created on the backend are generated on your frontend, just the ones that are required to communicate with your backend in any web service.