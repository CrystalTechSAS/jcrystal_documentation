# Password

This class is used to describe that an entity field is a password. In this way, jCrystal knows how it must be stored and retrieved. Please take into account that for the safety of your system, you can't access the exact value of a password value after it has been stored. 

Usually, is used in conjunction with the annotation `@HashSalt("randomString")`, which receives a random string to salt the password. You can read more about the salt [here](https://en.wikipedia.org/wiki/Salt_(cryptography)).

Usage on entities:

```java
import jcrystal.entity.types.security.Password;
...
@EntityProperty
@HashSalt("djhka123Ds")
private static Password password;
```

# FirebaseAccount
This class is used to describe a field that contains a [Firebase account](https://firebase.google.com/docs/auth). In this way, you can log in a user through Firebase and save the account information on an entity.

Usage:
```java
import jcrystal.entity.types.security.FirebaseAccount;
...
@EntityProperty
private static FirebaseAccount firebaseId;
```

If you want to learn more about using this class, please check [here](../auth.md).