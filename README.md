# jCrystal Framework (beta)
_jCrystal_ is a fullstack framework based on code generators. It aims to reduce code re-write on web applications by reusing backend side data structures, business logic and web services to generate frontend equivalents.

## What can you achieve with jCrystal?
On the Server Side:
- Build Restful Web Services endpoints and deploy them on a high available infraestructure.
- Build a Object-Relationship Model for your solution and deploy it on a Non-SQL Database.
- Process async job loads in a simple way.
- User validation. 

On the client side:
- Access your web services with zero effort.
- Access your Object-Relationship Model with zero effort.

Our beta allows you to write your backend in Java and deploy it over Google App Engine using Google Datastore database (legacy).

jCrystal has support for the following platforms:
- iOS 12^ (Using Swift 5)
- Android 6^ (Using Java 7^)
- Flutter (Using Dart)
- Angular 7^(Usign Typescript)
- jQuery (using JS)

## Getting Started
- [Installation](getting_started/installation.md)
- [Creating a new application](getting_started/creating_app.md)
- [Running and testing your application](getting_started/run_test.md) 
- [Anatomy of a jCrystal application](getting_started/anatomy.md) 
- [jCrystal's paradigm](getting_started/paradigm.md)
- [Troubleshooting](getting_started/troubleshooting.md)

<!--
## Tutorial
- Part 1: A simple blogging plataform backend
- Part 2: Adding a frontend client
- Part 3: Adding authenticated users
- Part 4: Setting an admin site
- Part 5: Queries and async tasks -->

## Basic guides

### Backend

<!--- - [General & Architecture](server/general.md) (optional)-->
- [Web Services](server/webservices.md)
- [Authentication  and Autorization](server/auth.md)
- [Entities and DB access](server/entities.md)
- [Async jobs, queues and crons](server/queues.md) (optional)

### FrontEnd

- [General](clients/general.md) (Must read!!!)
- [Angular 7](clients/angular7.md)
- [Android](clients/android.md)
- [iOS](clients/ios.md)
- [jQuery](clients/jQuery.md)


<!--- 
## Advanced topics:

- [Web Admin](server/queues.md)
--->