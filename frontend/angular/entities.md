# Entities

## Basics

jCrystal generates the .ts files of the entities (data model) required to communicate with the backend, you can find them in the jCrystal generated folder: `jcrystal/entities`. One jEntity (entity) will generate several related files on your Angular project: 

- One class that has all the attributes, methods to access them and change them as well as utility methods.
- One or more interfaces that specify the access level of the entity. This will help you know what level of detail will be required or received by the web service. 

For example, for a given entity `User` you could find these classes on Angular:

- `User.ts`: The class with all the attributes and methods to access those attributes.
- `UserMin.ts`: An interface with the minimum attributes of User.
- `UserBasic.ts`: An interface with the basic attributes of User.
- `UserNormal.ts`: An interface with the normal attributes of User.
- `UserDetail.ts`: An interface with the detailed attributes of User.
- `UserFull.ts`: An interface with all the attributes of User.

The "main" class, `User` class, will implement all the other available interfaces. 

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

Let's say that on the frontend you need to list all the users and show the name and last login; then, you don't need to receive all the attributes of the users, so the backend developer might say that the attributes Name and Last Login will comprise the "Min" level of the entity User; therefore, the generated interface `UserMin.ts` will contain only those attributes and methods to access and modify them. Additionally, the web service that gives you the list of all users on the frontend will return a list of the interface UserMin.

**So how does this help you?** When you have a service that returns a list of the interface UserMin, then for each User you only will be able to access their attributes Name and Last Login. In this way, jCrystal helps you avoid common mistakes, when you try to access attributes that the entity doesn't have.

### Using an entity
You can use the entity by accessing and modifying its attributes, for each attribute you will find two methods: `get<AttributeName>()` and `set<AttributeName>(...)`. 

For example, if you have an object of the type UserMin, that we proposed earlier, you would find these methods available.


```typescript
setName(name: string);
getName() : string;
setLastLogin(lastLogin: CrystalDateMilis);
getLastLogin() : CrystalDateMilis;
```

To check what is a `CrystalDateMilis`, please read the [next section](#crystal-dates).


Also, you can cast an object of the type of an interface to the "main" class. Like this:
```typescript
import { UserMin } from 'src/app/jcrystal/entities/UserMin';
import { User } from 'src/app/jcrystal/entities/User';
...
let userMin:UserMin = ...;
let user = (userMin as User);
```

Finally, always remember to **import** the class of your entity on the component or class that uses it.

### Utility classes
Coming soon :flushed:

## Special entities

### Crystal dates 
jCrystal has special classes to represent dates and times, they are generated on Angular automatically. Therefore, you will find in the jcrystal/entities folder these utility classes:

- `CrystalDate.ts`
- `CrystalDateMilis.ts`
- `CrystalDateSeconds.ts`
- `CrystalDateTime.ts`
- `CrystalTime.ts`
- `CrystalTimeMilis.ts`
- `CrystalTimeSeconds.ts`

The difference between them is the precision with which each one saves the date and time. As an example, `CrystalDateSeconds` takes into account the whole date and time with a precision of seconds, while `CrystalDateMilis` has a precision of milliseconds and `CrystalTime` only considers the time of the day and not the date. 

These classes are used to communicate with the server, either by sending parameters or receiving information. Therefore, the signature of each web service (or the type in each entity) will let you know which of these classes you should use. 

You can create a CrystalDate* instance using an object of type Date like this:

```typescript
import { CrystalDateMilis } from 'src/app/jcrystal/entities/CrystalDateMilis';
import { CrystalTime } from 'src/app/jcrystal/entities/CrystalTime';
...
const date: Date = new Date();
const crystalDateTime = new CrystalDateMilis(date);
const crystalTime = new CrystalTime(date);
```

Additionally, given a CrystalDate* class you can format the date to obtain a formatted string and a formatted human-readable string:

```typescript
import { CrystalDateMilis } from 'src/app/jcrystal/entities/CrystalDateMilis';
...
const date: Date = new Date();
const crystalDateTime = new CrystalDateMilis(date);

const strDate: string = crystalDateTime.format(); //Formated date with default format 'YYYYMMDDHHmmssSSS'
const strHumanDate: string = crystalDateTime.formatClient(); //Formated date with default human-readble format 'DD/MM/YYYY HH:mm'
```

You can also enter a [valid format](https://momentjs.com/docs/#/displaying/format/) as a parameter for the format method:

```typescript
import { CrystalDateMilis } from 'src/app/jcrystal/entities/CrystalDateMilis';
...
const date: Date = new Date();
const crystalDateTime = new CrystalDateMilis(date);

const strDate: string = crystalDateTime.format("DD.MM.YYYY HH:mm"); //Formated date with format 'DD.MM.YYYY HH:m'
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
