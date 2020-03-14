# jCrystal entity queries

## Overview

To do an Entity query you must use the inner type Query:

```java
YourEntity.Query
```

Following you can add query customizations:

- Count limits: How many entities will be retrive at least by the current query.
- Transactionability: If the query must run inside current transaction.
- Batch size: how many entities will be taken on each go to DB.

```java
YourEntity.Query.limit(100).txn()
```

The jCrystal entity system allows you to create queries over entity properties. The are three types of entity queries:

- Owner key based
- Single field based
- Compound Index based queries

## Owner key based

TBD

## Single field queries

Single field queries allows you to filter entities by single property values. You can make single value queries or range value queries (for sortable property types).

To enable single field queries you must add `index = IndexType.MULTIPLE` on `@EntityProperty` for the field you want to query. The following index:

```java
@jcrystal.reflection.annotations.jEntity
public class User {
	
	@EntityProperty(index = IndexType.MULTIPLE)
	private static String name;

}
```

Enables the following query:

```java
User.Query.name("simple name")
```

which retrieves a list of Users with the given name.

On sortable types like dates you can query on ranges:

```java
@jcrystal.reflection.annotations.jEntity
public class User {
	
	@EntityProperty(indexed = IndexType.MULTIPLE)
	private static CreationTimestamp creationTime;

}
```

Enabling the following query:

```java
User.Query.creationTime(new CrystalMonth().toDate(), new CrystalMonth().next().toDate())
```

which retrieves a list of Users created on current month.

### Index Types

You can use one of the following Index Types:

- IndexType.MULTIPLE: which retrieves a list of entities for each index value.
- IndexType.UNIQUE: which retrieves a single entity for each index value. jCrystal supposes that your will ensure each index value will have at most 1 entity.
- IndexType.UNIQUE_CHECK (TBS): which retrieves a single entity for each index value. jCrystal will check every put on this index an throw an Exception if a collision occurs.

## - Compound Index based queries
Como se indico previamente, las propiedades de una entidad pueden estar indexadas, en la caso de las propiedades de manera optativa y en el de las relaciones de manera automática.

Sin embargo, en algunos casos se necesita buscar registros no por el valor de un campo sino por la combinación de valores de varios campos, en estos casos la clase de la entidad se anota con `@EntityIndex` con los siguientes parámetros:
- _name_: nombre cual el cual se referirá
- _value_: Un arreglo de String con los nombres internos de los campos incluidos en el índice.

