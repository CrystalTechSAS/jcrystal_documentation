### Entidades con relaciones en los listados

En principio cuando se implementa el Manager de una entidad para el Administrador Web, el método list suele ser algo del siguiente estilo.

En ManagerMiEntidad.java:
```java
public static List<MiEntidad> list(){
    return MiEntidad.Query.getAll();
}
```

#### Cambios en la entidad que referencia
Pero MiEntidad tiene una relación con Usuario a través de un campo propietario.
```java
public class MiEntidad {
    //...
	@RelMto1
	private static Usuario propietario;
    //...
}
```

Por defecto los propiedades de una entidad de tipo relación no aparecen en las respuestas de los servicios pues no tienen un nivel de detalle asignado, indicamos entonces que el campo tendrá nivel de detalle normal.
```java
public class MiEntidad {
    //...
	@RelMto1(keyLevel=JsonLevel.NORMAL)
	private static Usuario propietario;
    //...
}
```

#### Cambios en la entidad referenciada.
La información que va a presentarse de la entidad referenciada en el administrador web es su conversión a String a través del método toString, entonces debemos Re implementarlo para que arroje un resultado significativo.
Por ejemplo:
```java
public class Usuario {
    //...
	public String toString() {
        return this.nombre();
    }
    //...
}
```

#### Cambios en el Manager con el servicio de lista.
En el Manager el método `list` debemos ahora:
- Usar la anotación `@JsonString` donde se indica que clases se convertiran en su representación como String
- Retornar una Tupla2 donde el primer elemento es la lista que se retornaba originalmente, y el segundo una lista con las entidades del tipo asociado, que podrían estar relacionadas con los objetos de MiEntidad.

El resultado seria el siguiente:
```java
@JsonString({User.class})
public static Tupla2<List<Pet>, List<User>> list(){
    return new Tupla2(Pet.Query.getAll(),User.Query.getAll());
}
```