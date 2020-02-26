# Entities

## Basics

jCrystal generates the .java files of the entities (data model) required to communicate with the backend, you can find them in the jCrystal generated folder: `jcrystal/mobile/entities`. One jEntity (entity) will generate several related files on your Android project: 

- One class that has all the attributes, methods to access them and change them as well as utility methods. The name of that class is the same name of the entity; for example, `User.java`. 
- One or more interfaces that specify the access level of the entity. This will help you know what level of detail will be required or received by the web service. The name of that classes are the same name of the entity followed by a the level; for example, `UserNormal.java`.  
- One class with methods to store, retrieve and delete an entity or array of the entities in the local database. The name of that class is the `DB` followed by the name of the entity; for example, `DBUser.java`.  

For example, for a given entity `User` you could find these classes on Android:

- `User.java`: The class with all the attributes and methods to access those attributes.
- `UserMin.java`: An interface with the minimum attributes of User.
- `UserBasic.java`: An interface with the basic attributes of User.
- `UserNormal.java`: An interface with the normal attributes of User.
- `UserDetail.java`: An interface with the detailed attributes of User.
- `UserFull.java`: An interface with all the attributes of User.
- `DBUser.java`: Class used to store, retrieve and delete an entity or array of the entities in the local database.

The "main" class, `User.java` class, will implement all the other available interfaces. 

Please take into account that for a given entity some of those interfaces might be generated and some not. 

**What's the use of the interfaces?** Every web service that returns an entity, will, in fact, return an interface of that entity, in this way you know the attributes that the backend sends you. 

**So, who decides which attributes have each interface and which service returns what interface?** The backend developer: he decides which attributes will be sent for each web service. 

As an example, if an entity User has these attributes:
- Name
- Gender
- Birthdate
- Date created
- Last login
- Country
- City
- Favorite color

Let's say that on the frontend you need to list all the users and show the name and last login; then, you don't need to receive all the attributes of the users, so the backend developer might say that the attributes Name and Last Login will comprise the "Min" level of the entity User; therefore, the generated interface `UserMin.java` will contain only those attributes and methods to access and modify them. Additionally, the web service that gives you the list of all users on the frontend will return a list of the interface UserMin.

**So how does this help you?** When you have a service that returns a list of the interface UserMin, then for each User you only will be able to access their attributes Name and Last Login. In this way, jCrystal helps you avoid common mistakes, when you try to access attributes that the entity doesn't have.


### Using an entity
You can use the entity by accessing and modifying its attributes, for each attribute you will find two methods a getter and a setter.

For example, if you have an object of the type User, that we proposed earlier, you would find these methods available for the attribute `name`.

```java
public class User {
    ...
    public String name(){...}
    public void name(String val) {...}
    ...
}
```

So, you can use them like this:
```java
import jcrystal.mobile.entities.User;
...
User user = new User();
user.name("Jane Doe");
String theName = user.name(); //The name of your user
```

Additionally, objects of the type of the interfaces allow you to access the attributes. As an example, an object of type UserMin would have this methods:

```java
public class UserMin {
    String name();
    CrystalDateMilis getLastLogin();
}
```
To check what is a `CrystalDateMilis`, please read the [next section](#crystal-dates).


Also, you can cast an object of the type of an interface to the "main" class. Like this:
```java
import jcrystal.mobile.entities.User;
import  jcrystal.mobile.entities.UserMin;
...
UserMin userMin = ...;
User user = (User)userMin;
```

Finally, always remember to **import** the class of your entity on the component or class that uses it.

### Saving and retriving entities in the local Database 
Each jEntity generates a file named `DB<jEntityName>` where you can find methods to store, retrieve and delete an entity or array of the entities in the local database. 

To use these methods the only thing required is to keep a **key** that will identify the element being stored and will help to store it and delete it. 

In each `DB<jEntityName>` file you will find this **public static** methods:

- `boolean store(String key, <jEntityName> value)`: Method to store an entity with a key. The method returns true if the storage was successful. 
- `boolean store(String key, java.util.List<jEntityName> values)`: Method to store a list of entities with a key. The method returns true if the storage was successful. 
- `<jEntity> retrieve(String key)`: Method to retrieve the entity given a key. 
- `java.util.List<jEntityName> retrieveList(String key)`: Method to retrieve an entity list from given a key. 
- ` void delete(String key)`: Method to delete the object saved on the key.

Therefore, given an entity you can store it, retrieve it and delete it from the local database. For example, consider the entity User defined previously:

```java
import jcrystal.mobile.entities.User;
import jcrystal.mobile.entities.DBUser;

...
User user = new User();
user.name("Jane Doe");
DBUser.store("myUser");
....
User myUser = DBUser.retrieve("myUser");
```

### Utility classes
Coming soon :flushed:

## Special entities

### Crystal dates 
jCrystal has special classes to represent dates and times, which come with our library:

- `CrystalDate.java`
- `CrystalDateMilis.java`
- `CrystalDateSeconds.java`
- `CrystalDateTime.java`
- `CrystalTime.java`
- `CrystalTimeMilis.java`
- `CrystalTimeSeconds.java`

The difference between them is the precision with which each one saves the date and time. As an example, `CrystalDateSeconds` takes into account the whole date and time with a precision of seconds, while `CrystalDateMilis` has a precision of milliseconds and `CrystalTime` only considers the time of the day and not the date. 

These classes are used to communicate with the server, either by sending parameters or receiving information. Therefore, the signature of each web service (or the type in each entity) will let you know which of these classes you should use. 

The CrystalDate* classes extend `java.util.Date` so you can create a date like this:

```java
import jcrystal.datetime.CrystalDate;
import jcrystal.datetime.CrystalTime;
import jcrystal.datetime.CrystalDateMilis;
...
CrystalDate date = new CrystalDate(); //Crystal Date with the current date. 
CrystalDateTime crystalTime = new CrystalTime(System.currentTimeMillis()); //You can create a CrystalDate* from a given time in miliseconds. 
CrystalDateMilis date = new CrystalDateMilis(); 
```

Additionally, given a CrystalDate* class you can format the date to obtain a formatted string and a formatted human-readable string:

```java
import jcrystal.datetime.CrystalDateMilis;
...
CrystalDateMilis date = new CrystalDateMilis(); 
String strDate = date.format(); //Formated date with default format 'yyyyMMddHHmmssSSS'
String strHumanDate = date.toSimpleDateTimeFormat(); //Formated date with default human-readble format 'dd/MM/yyyy HH:mm'
```

Since the CrystalDate* classes extend `java.util.Date` you can format them using a `SimpleDateFormat`:

```java
import jcrystal.datetime.CrystalDateMilis;
...
CrystalDateMilis date = new CrystalDateMilis(); 
SimpleDateFormat simpleDateFormat = new SimpleDateFormat("dd.MM.yyyy HH:mm");
String strDate = simpleDateFormat.format(date); //Formated date with format 'dd.MM.yyyy HH:mm'
```

### Token entity

jCrystal uses a custom token session management by configuring a `<TokenEntity>` (where `<TokenEntity>` is a name such as `Token`) entity that will manage the session token. Whenever such configuration is made, that entity will be generated on the frontend with the usual methods of the generated entities, but also methods related to the user authentication:

- `store<TokenEntity>()`: Method to store and cache in your local database this entity.
- `get<TokenEntity>()`: Method to get from your cache or your local database this entity.
- `delete<TokenEntity>()`: Method to delete the entity of the local database and cache.
- `isAuthenticated()`: Method to know if the user is authenticated in the app.

jCrystal automatically:
- Saves the token in a local database whenever the token is received from the backend.
- Sends the token in the web services that require authentication. 

Therefore, as a frontend developer your responsibility related to the authentication will be to:

- Check if the user is authenticated to show him the appropriate information.  
This can be done by using the method `isAuthenticated()` of the `<TokenEntity>` class.

- Delete the `<TokenEntity>` from the local database whenever the user logs out of the system.  
This can be done by using the method `delete<TokenEntity>()` of the `<TokenEntity>` class.


Please take into account that this class will be generated only if the backend configures an entity for the token session management.
