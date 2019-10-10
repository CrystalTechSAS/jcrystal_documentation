# jCrystal Framework (beta)
_jCrystal_ is a fullstack framework based on code generators. It aims to reduce code re-write on web applications by reuseing backend side data structures, business logic and web services to generate frontend equivalents.

## What can you achieve with jCrystal?
On the Server Side:
- Build a Object-Relactionship Model for yours clases and deploy it on a Non-SQL Database.
- Bulld Restful Web Services endpoints and deploy them on a HA infrasestructure.
- Process async job loads in a simple way.
- Validación de usuarios.

* Our MVP allows you to write your backend in Java and deploy it over Google App Engine using Google Datastore database (legacy).

On the Client Side:
Los *endpoints* se pueden generar como:
- Swift para iOs
- Java para Android
- Typescript para plataformas web (especialmente Angular2)

jCrystal have support for the following platforms:
- iOS 12^ (Using Swift 5)
- Android 6^ (Using Java 8^)
- Flutter (Using Dart)
- Angular 7^(Usign Typescript)
- jQuery (using JS)

## Installation

- [Using Eclipse](Installation.md)

## Basic guides

### Backend

- [General & Architecture](server/general.md) (optional)
- [Web Services](server/webservices.md)
- [Entities and DB](server/entities.md)
- [Queues and Crons](server/queues.md) (optional)

### FrontEnd

- [*General](clients/angular7.md) (Must read!!!)
- [Angular 7](clients/angular7.md)

## Advanced topics:

- [Web Admin](server/queues.md)

## jCrystal layers:
We propose (an generate?) 3 simple layers:

- A data access layer: it allows access to stored data in all platforms.
- A connection layer: composed by RestfulWS, it allows communication between platforms
- Buisiness layer?
