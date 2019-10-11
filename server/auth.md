# JCrystal authentication

jCrystal MVP uses a custom token session management. In order to use it you must:

1. Create an entity for your session token(s).

```java
package company.example.entities.security;
...
@Entidad @LoginResultClass
public class Token implements SecurityToken{
	@EntityKey
	private static final String token = null;
	@EntityProperty
	private static long rol;
    ...
}
```