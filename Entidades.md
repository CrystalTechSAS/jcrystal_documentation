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

Entre los metodos que genera JCrystal para los campos estan los _getters_ y los _setters_ de cada uno de los campos.

Para que un campo sea __requerido en el constructor__, su especificación debe especificar con la palabra clave _final_.

#### Propiedades
Las propiedades de la entidad son aquellos campos que no expresan una relación con otra entidad, sus tipos pueden ser:
- Tipos primitivos de Java (excepto arreglos)
- String
- Email -TODO- Clase exacta
- los _wrapper_ de JCrystal para las fechas (CrystalDate).
- Arreglos de enteros

Se denotan con la anotación `@jcrystal.reflection.annotations.EntityProperty`

-TODO- Preguntar GA tipos soportados

##### Parametros
La anotación `@jcrystal.reflection.annotations.EntityProperty` tiene los siguientes parametros.
- _name_ (String): nombre interno que se usara para el campo el la tabla del Datastore.
- _unique_ (booleano): indica si se espera que solo haya un resultado por cada valor de la propiedad, los metodos de consulta usando esta propiedad retornaran un solo resultado en vez de una lista de ellos.
- _indexed_ (booleano): Indica si la variable esta indexada, lo cual es requisito para que se puedan buscar en la base de datos registros con un valor especifico de la misma.
- _editable_
- _json_
- _autoNow_ (booleano): aplicable solo a los parametros de tipos CrystalDate*, indica si estos se inicializan automaticamente con el tiempo actual.

#### Relaciones
Las relaciones son campos de una entidad que la asocian con otra, pueden ser '1 a 1', 'muchos a muchos' o 'muchos a 1', estos campos se denotan con las siguientes anotaciones [todas del paquete `jcrystal.reflection.annotations.entities`]:
- `@Rel1to1`
- `@RelMto1`
- `@RelMtoM`

Todas comparten los mismos parametros:
- _name_(String): equivalente al parametro del mismo nombre en las propiedades
- _target_(String): nombre del pseudo-campo que se creara en la entidad referida con la relación inversa.
- _keyLevel_: equivalente al parametro _json_ en las propiedades
- _editable_(boolean): equivalente al parametro del mismo nombre en las propiedades

Los campos de relacion, son indexados automaticamente y por tanto no tienen la opción _indexed_.

### Indices
Como se indico previamente, las propiedades de una entidad pueden estar indexadas, en la caso de las propiedades de manera optativa y en el de las relaciones de manera automatica.

Sin embargo, en algunos casos se necesita buscar registros no por el valor de un campo sino por la combinación de valores de varios campos, en estos casos la clase de la entidad se anota con `@EntityIndex` con los siguientes parametros:
- _name_: nombre cual el cual se referira
- _value_: Un arreglo de String con los nombres internos de los campos incluidos en el indice.

## Niveles de acceso
Los campos de una entidad pueden tener niveles de detalle que especifican subconjuntos de campos con los que se puede presentar el objeto.  Un nivel de detalle incluye  todos los niveles inferiores, p.e: si se pide un objeto con nivel de detalle NORMAL, este uncluira tambien los campos con nivel MIN y BASIC.

Estos son los niveles posibles en **orden**, especificados en el _enum_ `jcrystal.json.JsonLevel`; a saber:
- MIN
- BASIC
- NORMAL: el nivel de acceso por defecto
- DETAIL
- FULL
Adenas hay tres niveles especiales.
- NONE: Indica que el campo no se debe incluir en ninguna presentación del objeto.
- ID: solo el identificador.
- TOSTRING: el identificador y el resultado del metodo `toString()` de la entidad.
- DEFAULT: **No debe usarse**, lo usa JCrystal internamente.

En el caso de las propiedades el nombre del parametro es _json_, en el de las relaciones _keyLevel_.

_Nota:_ estos niveles de acceso se usan de manera paralela en los servicios.

## Metodos
Tras la primera ejecución de JCrystal se pueden implementar metodos auxiliares que no seran modificados por JCrystal.

### Metodos de inicializaciën @jcrystal.reflection.annotations.entities.OnConstruct
Los metodos anotados con `@OnConstruct` son llamados desde el constructor del objeto y se usan comunmente para inicializar el valor de las propiedades.

### Representación como cadena de texto toString
Cuando se usa el nivel de acceso JsonLevel.TOSTRING, el objeto resultante solo contiene el resultado de su metodo toString y su identificador.

### Metodos generados

#### Constructor

#### Setters y getters

## Funciones de consulta
Subclase Query
### Subclase query

## Objetos DAO, según niveles de acceso.