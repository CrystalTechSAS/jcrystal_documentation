# JCrystal authentication

jCrystal MVP uses a custom token session management. In order to use it you must:

1. Create an entity for your session token(s).

```java
package company.example.entities.security;
...
@jEntity @LoginResultClass
public class Token implements SecurityToken{
	@EntityKey
	private static final String token = null;//The entity key must be named token
    ...
}
```

2. Run jCrystal.
3. Make a login WS:

```java
package company.example.controllers;

public class Manager {
	public static Token sampleLogin(String username, String password){
		return Token.generateTokenBase64("Some custom/random string" + username /* some user especific data*/)
			.put();
	}
}
```

4. Recieve session tokens on your webs services:

```java
package company.example.controllers;

public class Manager {
	public static String helloworld(Token token){
		return "Hello World from jCrystal!";
	}
}
```

This WS can only be called by an authenticated user.

## Adding user data to session tokens

It is common and usefull to add user especific data to session tokens. The most common case is that you want to know which user is owner of each token. This is a simple task on jCrystal. the following class examples shows you how to have a basic username/password authentication:

```java
...
@jEntity
public class User{
	
	@EntityProperty(index=IndexType.UNIQUE_VERIFICATION)
	private static String username;
	
	@EntityProperty 
	@HashSalt("random string")
	private static Password password;
    ...
}
```

```java
...
@jEntity @LoginResultClass
public class Token implements SecurityToken{
	@EntityKey
	private static final String token = null;
	@Rel1to1
	private static User user;
    ...
}
```

```java
...
public class Manager {
	public static Token login(String username, String password){
		User userEntity = User.Query.Username.get(username);
		if(userEntity == null || !userEntity.validatePassword(password))
			throw new ErrorException("Invalid username or password");
		return Token.generateTokenBase64("Some custom/random string" + username)
			.user(userEntity)
			.put();
	}
}
```

### Sign up 

```java
...
public class Manager {
	public static void signup(String username, String password){
		if(User.Query.Username.get(username) != null)
			throw new ErrorException("User already exists");
		new User()
			.username(username)
			.password(password)
			.put();
	}
}
```

## Advanced sign in methods

TBD