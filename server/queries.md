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

- Primary key based
- Single field based
- Compound Index based queries
- Full search queries (TBD)

## Primary key based

TBD

## Single field queries

Single field queries allows you to filter entities by single property values. You can make single value queries or range value queries (for sortable property types).

To enable single field queries you must add `index = IndexType.MULTIPLE` on `@EntityProperty` for the field you want to query. The following index:

```java
public class User {
	
	@EntityProperty(index = IndexType.MULTIPLE)
	private static String name;

}
```

Enables the following query:

```java
User.Query.name("Bob")
// Retrieves a list of Users with Bob as name.
```

On sortable types like dates you can query on ranges:

```java
public class User {
	
	@EntityProperty(indexed = IndexType.MULTIPLE)
	private static CreationTimestamp creationTime;

}
```

Enabling the following query:

```java
User.Query.creationTime(new CrystalMonth().toDate(), new CrystalMonth().next().toDate())
// Retrieves a list of Users created on current month.
```

### Index Types

You can use one of the following Index Types:

- IndexType.MULTIPLE: which retrieves a list of entities for each index value.
- IndexType.UNIQUE: which retrieves a single entity for each index value. jCrystal supposes that your will ensure each index value will have at most 1 entity.
- IndexType.UNIQUE_CHECK (TBS): which retrieves a single entity for each index value. jCrystal will check every put on this index an throw an Exception if a collision is detected.

## - Compound Index based queries

You can make complex queries by defining special indexes. A special index can be defined over each enity using the `@_Entity_Index` annotation. This annotation recieves two params:
- name: The index name
- fields: An array with the fields that compose the index.

The next snippet shows how to create a compound index for User:

```java
@UserIndex(name = "byNameCreation", fields = {F.name, F.creation})
public class User {
	
	@EntityProperty(index = IndexType.MULTIPLE)
	private static String name;

	@EntityProperty(indexed = IndexType.MULTIPLE)
	private static CreationTimestamp creationTime;

}
```

This index enables you to query users with a a given name and a creation time:

```java
User.Query.byNameCreation("Bob", new CrystalDateTime().toDate())
// Retrieves a list of users named Bob which has been created on a specific millisecond
```

You can also make range queries:

```java
User.Query.byNameCreation("Bob", new CrystalMonth().toDate(), new CrystalMonth().next().toDate())
// Retrieves a list of users named Bob which has been created on current month
```

> :warning: **Only indexed properties can be used on compound index definitions**

