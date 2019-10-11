# jCrystal entity queries

## Single field queries

Para poder filtrar una _Entidad_ por un campo este debe estar indexado, esto se logra con el parámetro indexed colocado en true en la anotación `@EntityProperty` así:
`@EntityProperty(indexed = true)`


### Índices
Como se indico previamente, las propiedades de una entidad pueden estar indexadas, en la caso de las propiedades de manera optativa y en el de las relaciones de manera automática.

Sin embargo, en algunos casos se necesita buscar registros no por el valor de un campo sino por la combinación de valores de varios campos, en estos casos la clase de la entidad se anota con `@EntityIndex` con los siguientes parámetros:
- _name_: nombre cual el cual se referirá
- _value_: Un arreglo de String con los nombres internos de los campos incluidos en el índice.

