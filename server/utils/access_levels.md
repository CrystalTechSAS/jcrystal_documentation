# Access levels
Entities can have levels of detail that specify subsets of fields with which the object can be presented. This is useful to answer in each web service the required information of an entity and not every property of the entity.

A level of detail includes all lower levels, for example: if an object with NORMAL level of detail is requested, it will also include the fields with MIN and BASIC level.

These are the levels in **order**, specified in the _enum_ `jcrystal.json.JsonLevel`:
- MIN
- BASIC
- NORMAL: The default level of an entity property.
- DETAIL
- FULL

Additionally there are three special levels:
- NONE: Specifies that the property should not be included in any presentation of the object.
- ID: the identifier of the entity. :flushed:
- TOSTRING: the identifier and result of the entity's `toString ()` method.
- DEFAULT: **Do not use**, it's used internally by JCrystal.

The name of the parameter to specify the level in the properties is _json_. On the other hand, the name of the parameter to specify the level in the relationships is _keyLevel_.

_Note: _ these access levels are used in the webservices.