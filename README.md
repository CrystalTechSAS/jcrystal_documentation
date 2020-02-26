# jCrystal Framework (beta)
jCrystal is a framework to build **full-stack platforms** more **quickly** and with **less** code.

## What can you achieve with jCrystal?
jCrystal makes it easier to build **long-lasting backends**:

- **RESTful web services made easy**: One method is one web service, that's all. 

- **Straightforward database storage and access**: Write your data model, jCrystal does everything else. 

- **Painless user authentication and authorization**: Authenticate your users, manage their sessions and authorize their actions without all the hassle. 

- **Admin site**: Easily get an admin interface to manage the content of your backend.

- **Effortlessly** build your backend over a **highly-scalable NoSQL database and a highly-available infrastructure**.

jCrystal helps you build **frontend apps on top of your backend** (or any backend):

- **Painless consumption of web services**: jCrystal generates the code to easily integrate with your web services. 


- **Effortless access to your data model**: jCrystal generates your data model on your frontend language. 

- **Simple access to the local database:** jCrystal stores and retrieves your data model on your frontend, no need to worry about your local database anymore. 

jCrystal does this and more because it's a framework based on **code generators**. In this way, jCrystal reduces code re-write web and mobile applications by reusing backend side data structures, business logic, and web services to generate frontend equivalents.

jCrystal has support for the following platforms:
- iOS 12^ (Using Swift 5)
- Android 6^ (Using Java 7^)
- Angular 7^(Usign Typescript)
- jQuery (using JS)
- Flutter (Using Dart)

Our beta allows you to write your backend in Java and deploy it over Google App Engine using Google Datastore database (legacy).

## Getting Started
### Backend
- [Installation](getting_started/installation.md)
- [Creating a new project](getting_started/creating_project.md)
- [Running and testing your project](getting_started/run_test.md)
- Create a hello world with a client (backend + frontend):
    - [Angular](getting_started/hello_clients/angular.md)
    - [Android](getting_started/hello_clients/android.md)
- [Anatomy of a jCrystal project](getting_started/anatomy.md) 
- [jCrystal's paradigm](getting_started/paradigm.md)
- [Troubleshooting](getting_started/troubleshooting.md)

### Frontend
- [Working with jCrystal on the frontend (must read)](getting_started/working_frontend.md)
- Setup your frontend app:
    - [Angular 7](frontend/angular/setup.md)
    - [Android](frontend/android/setup.md)
    - [iOS](frontend/iOS/setup.md)

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
<!-- - [General](server/clients/general.md) (Must read!!!) -->

### Frontend
- [Angular 7](frontend/angular/general.md)
- [Android](frontend/android/general.md)
- [iOS](frontend/iOS/setup.md)
- [jQuery](frontend/jQuery.md)


<!--- 
## Advanced topics:

- [Web Admin](server/queues.md)
--->