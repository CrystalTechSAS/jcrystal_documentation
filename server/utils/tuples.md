# Tuples
A tuple is a sequence of final Java objects. Right now jCrystal supports tuples of up to 10 objects. Inside jCrystal dependencies you will find the `Tupla*` classes:

- `Tupla2.java`
- `Tupla3.java`
- `Tupla4.java`
- ...
- `Tupla10.java`

Where each number indicates how many objects the tuple contains.

Tuples were created on jCrystal to be able to return multiple objects in a web service. As an example, consider a website like Twitter, which has multiple users and multiple tweets, and think of a web service that given a word returns all the users and all the tweets related to that word. Therefore, the web service will receive one word and return a list of User entities and a list of Tweet entities that are related to that word. In a case like this, this web service can return a Tuple with 2 objects: lists of Users and lists of Tweets.

## Usage
You can create a `Tupla*` by calling its constructor, it receives the objects that the tuple will contain in the constructor:

```java
import jcrystal.results.Tupla2;
...
Tupla2<String, Integer> tuple = new Tupla2<>("Hello", 1);
```

You can access the objects that the tuple contains with the properties `v*` of the tuple, which go from `v0` to `v<tuple length - 1>`: 


```java
import jcrystal.results.Tupla2;
...
Tupla2<String, Integer> tuple = new Tupla2<>("Hello", 1);
String str = tuple.v0;
Integer inte = tuple.v1;
```
Remember that tuples contain final objects, so you can't change the objects inside the tuple after you have created it. 

Finally, you can append elements to a tuple:

```java
import jcrystal.results.Tupla2;
import jcrystal.results.Tupla3;
...
Tupla2<String, Integer> tuple = new Tupla2<>("Hello", 1);
Tupla3<String, Integer, Integer> tuple3 = tuple.append(2);
```
