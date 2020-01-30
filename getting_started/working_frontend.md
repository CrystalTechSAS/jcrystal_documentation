# Working with jCrystal

jCrystal is a full-stack framework that aims to reduce code rewrites, moreover, on your frontend clients it will help you:

- Access your web services with zero effort.
- Access your data model with zero effort.

This will be possible thanks to the code that jCrystal generates using the **descriptions of the web services and entities of the backend**. As such, please take into account that to use jCrystal on your frontend you **must** have a backend in jCrystal that has and uses frontend clients. If you already have a backend, please read [this guide to learn how to add clients to your backend](../clients/general.md).


jCrystal generates utility code usually in one folder and one or more sets of files depending on the frontend platform.  As a frontend developer, this means that:

- You are in charge of creating your frontend project.

    jCrystal will make everything easier for you, but you are still in charge of creating your frontend project. Don't worry, that only means you can customize it as much as you want!

    That also means jCrystal can be used on a frontend project that's already created.

- You **can use your own code editor for your frontend client**.

    Feel free to use the code editor that you are most familiar with on your client-side. jCrystal is here to make you **faster**, not to force you to change everything you know about frontend development

- You are in charge of setting up the project to support jCrystal.

    Don't worry, this usually means adding a couple of dependencies to your frontend project. :wink:


## Entities
jCrystal entities will be generated on the client folder whenever a web service annotated with the generated client annotation receives or returns a jEntity.

One jEntity will generate several related files on the client: 
- One class that has all the attributes, methods to access them and change them as well as helpful utility methods.
- One or more interfaces that specify the access level of the entity. This will help you know what level of detail will be required or received by the web service. 
- One class to manage the local storage of the entity. (Only available on Android and iOS)


### Entity access levels
//TODO: How to use the levels.

### Local Database (Only available on Android and iOS)
Each jEntity generates a file named `DB<jEntityName>` where you can find methods to store, retrieve and delete an entity or array of the entities in the local database. To use these methods the only thing required is to keep a key that will identify the element being stored and will help to store it and delete it. 

// TODO: Part keys. 

### Token Entity
jCrystal uses a custom token session management by configuring a `<TokenEntity>` (where `<TokenEntity>` is name such as `Token`) entity that will manage the session token. Whenever such configuration is made that entity will be generated on the client side with the usual methods of generated entities but also methods related to the user authentication:

- `store<TokenEntity>()`: Method to store and cache in your local database this entity.
- `get<TokenEntity>()`: Method to get from your cache or your local database this entity.
- `delete<TokenEntity>()`: Method to delete the entity of the local database and cache.
- `isAuthenticated()`: Method to know if the user is authenticated in the app.

jCrystal automatically saves and sends the token from the client side whenever the token is received from the server or required by it to consume a web service. Therefore, as a developer your responsibility related with the authentication will be to check if the user is authenticated to show him the appropriate information and delete the `<TokenEntity>` from the local database whenever the user logs out of the system. 

### Utilities

There are several entity utilites that can help to manage arrays of given entity: 

- Sort
- MapList
- Group
