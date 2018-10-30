# Entidades
## Introduccióm
Una entidad en JCrystal comienza como una clase con la definición de un objeto con ciertas propiedades, relaciones y comportamientos; las instancias de esta entidad se almacenaran en un tabla en un Datastore de GAE.

### Nota sobre la generación del código
Una parte del codigo que genera JCrystal para la entidad se crea dentro del mismo archivo de clase que contiene la definición.

Este codigo generado se coloca dentro de unos comentarios que delimitan la sección generada, para que en ejecuciones posteriores del generador de código se sobreescriba solo la región generada.

Un ejemplo:
```java
@Entidad
public class Room {
  //Aqui se encuentra la especificación.
/* GEN */
 //Aqui se encuentra el codigó generado.
/* END */
}
```

## Especificación
Para indicar que una clase es una entidad de JCrystal, se debe anotar con `@jcrystal.reflection.annotations.Entidad`
-TODO- Parametros.

### Campos de la entidad
Los campos de la entidad se especifican con atributos estaticos; para evitar confusiones, se recomienda que se declaren como `private`.

Entre los metodos que genera JCrystal para los campos estan los _getters_ y los _setters_.

#### Propiedades
Las propiedades de la entidad son aquellos campos que no expresan una relación con otra entidad, sus tipos pueden ser:
- Tipos primitivos de Java (excepto arreglos)
- String
- Email -TODO- Clase exacta
- los _wrapper_ de JCrystal para las fechas (CrystalDate).

Se denotan con la anotación `@jcrystal.reflection.annotations.EntityProperty`

-TODO- Preguntar GA tipos soportados

##### Parametros
Esta anotación tiene los siguientes parametros.
- _name_ (String): nombre interno que se usara para el campo el la tabla del Datastore.
- _unique_ (booleano): indica si se espera que solo haya un resultado por cada valor de la propiedad, los metodos de consulta usando esta propiedad retornaran un solo resultado en vez de una lista de ellos.
- _indexed_ (booleano): Indica si la variable esta indexada, lo cual es requisito para que se puedan buscar en la base de datos registros con un valor especifico de la misma.
- _editable_
- _json_
- _autoNow_ (booleano): aplicable solo a los parametros de tipos CrystalDate*, indica si estos se inicializan automaticamente con el tiempo actual.

#### Relaciones
Las relaciones son campos de una entidad que la asocian con otra, pueden ser '1 a 1' o 'muchos a muchos'.

Los campos de relacion, son indexados automaticamente.

### Indices
Como se indico previamente, las entidades 

## Niveles de acceso
jcrystal.json.JsonLevel

## Metodos

### Metodos de inicializaciën @jcrystal.reflection.annotations.entities.OnConstruct
Los metodos anotados con `@OnConstruct` son llamados desde el constructor del objeto y se usan comunmente para inicializar el valor de las propiedades.

### Representación como cadena de texto toString
Cuando se usa el nivel de acceso JsonLevel.TOSTRING, el objeto resultante solo contiene el resultado de su metodo toString y su identificador.



## Funciones de consulta
Subclase Query
### Subclase query

## Objetos DAO, según niveles de acceso.