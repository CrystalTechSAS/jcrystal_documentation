# Crystal Dates 
jCrystal has special classes to represent dates and times. Therefore, whenever you need to represent a date or time in a web service or entity, instead of using the class `java.util.Date` or any other, you must use one of the `CrystalDate*` classes which come with our dependencies:

- `CrystalDate.java`
- `CrystalDateMilis.java`
- `CrystalDateSeconds.java`
- `CrystalDateTime.java`
- `CrystalTime.java`
- `CrystalTimeMilis.java`
- `CrystalTimeSeconds.java`

The difference between each of them is the precision with which each one saves the date and time. As an example, `CrystalDateSeconds` takes into account the whole date and time with a precision of seconds, while `CrystalDateMilis` has a precision of milliseconds and `CrystalTime` only considers the time of the day and not the date. 

Whenever you are going to use one of these classes please do a careful selection considering the precision of the date and time that you need. If you are not sure, use   `CrystalDateMilis`. 

## Usage
You can create a `CrystalDate*` by calling its constructor which initializes the object so that it represents the time at which it was created:

```java
import jcrystal.datetime.CrystalDateMilis;
import jcrystal.datetime.CrystalTimeMilis;

...
CrystalDateMilis date = new CrystalDateMilis(); //Current date and time
CrystalTimeMilis time = new CrystalTimeMilis(); //Current time
```

Additionally, you can also create a `CrystalDate*` from a number of miliseconds, the object created is initialized it to represent the specified number of milliseconds since January 1, 1970, 00:00:00 GMT.

```java
import jcrystal.datetime.CrystalDateMilis;
import jcrystal.datetime.CrystalTimeMilis;

...
CrystalDateMilis date = new CrystalDateMilis(1583204463675);
CrystalTimeMilis time = new CrystalTimeMilis(1583204463675);
```

Given a `CrystalDate*` object, you can add a specified amount (signed) of miliseconds to it or add an specified (signed) amount of time to a given [calendar field](https://docs.oracle.com/javase/7/docs/api/java/util/Calendar.html):
```java
import jcrystal.datetime.CrystalDateMilis;
import java.util.Calendar;

...
CrystalDateMilis date = new CrystalDateMilis();
date = date.add(60 * 1000); //Adds 60 seconds to the date
date = date.add(Calendar.MONTH, 3); //Adds 3 months to the date
```

You can also obtain a `java.util.Date` object equivalent of your `CrystalDate*` object:

```java
import jcrystal.datetime.CrystalDateMilis;
import java.util.Date;

...
CrystalDateMilis date = new CrystalDateMilis();
Date javaDate = date.toDate();
```

Finally, you can also create a `CrystalDate*` object from a `String` and get a formatted String from a `CrystalDate*` object. 

```java
import jcrystal.datetime.CrystalDate;
import java.util.Date;

...
CrystalDate date = new CrystalDate("201910201010");// yyyyMMddHHmm is the format for the CrystalDate class. 
//date is intialized to 20th of October of 2019 at 10:10
String strDate = date.format(); // strDate = "201910201010"
```

However, please take into account the next table with the format of each `CrystalDate*` class, because **each `CrystalDate*` class has a different format**. 

| Class     | Format          | Level of detail          |
| ------------- |-------------|-------------|
| `CrystalDate.java` | "yyyyMMddHHmm" | Date and time with precision of minutes|
| `CrystalDateMilis.java` | "yyyyMMddHHmmssSSS" | Date and time with precision of miliseconds|
| `CrystalDateSeconds.java` | "yyyyMMddHHmmss"  | Date and time with precision of seconds |
| `CrystalDateTime.java` | "yyyyMMddHHmm"| Date and time with precision of  minutes|
| `CrystalTime.java` | "HHmm" | Time with precision of minutes|
| `CrystalTimeMilis.java` | "HmmssSSS"  | Time with precision of miliseconds |
| `CrystalTimeSeconds.java` | "HHmmss" | Time with precision of seconds |
