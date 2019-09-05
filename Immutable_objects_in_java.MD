# Immutable Objects in Java

> An object is considered immutable if its state cannot change after it is constructed.

## How to define immutable objects 
Make the class final, and don’t provide any methods to modify the fields. 

A final class is simply a class that can't be extended and by doing so we make sure that there won' be any subclasses to override the methods.

Another way to do this is by making the constructor private and construct instances in factory methods ( If you make only a private constructor, no class can extend your class, because it can't call the super() constructor )

```java
// make this class final, no one can extend this class
public final class ImmutableExample {

	private String name;

	ImmutableExample (String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	//no setter
	
	public static void main(String[] args) {

		ImmutableExample obj = new ImmutableExample("harshajayamanna.com");
		System.out.println(obj.getName());

		// there is no way to update the name after the object is created.
		// obj.setName("somedomain.com");
		// System.out.println(obj.getName());

	}
}
```

## Why String is immutable ?

This is a popular example when talking about Immutability. I had to put a greate effort to find a proper example to understand this.

To understand this, first let us create a string
```java
String str = "knowledge";
```
This creates a string containing "knowledge" and assigns it a reference str. Lets perform some more functions
```java
String s = str;     // assigns a new reference to the same string "knowledge"
```
![String_Constant_Pool](https://raw.githubusercontent.com/h-hub/blog_resources/master/String%20Constant%20Pool.jpg)


Lets see how the below statement works:
```java
str = str.concat(" is power");
```
This appends a string " base" to str. Since string objects are immutable it doesn't really append. What happens under the hood is, it creates a new string by getting the value of str and " is power". The new string is "knowledge is power". Finally the jvm assign this string to str. Now the string constant pool would look like this.
![String_Constant_Pool2](https://raw.githubusercontent.com/h-hub/blog_resources/master/String%20Constant%20Pool2.jpg)
Here, the " is power" string is considered lost because it does not have a reference.

This can be understood more clearly if you look at the source code of concat method of java.lang.String.
```java
//concat method
```
### String constant pool
String literals could occupy large area of memory in an Application and String constant pool helps to save memory and make the application efficient.

When the compiler sees a String literal, it looks for the String in the pool. If a match is found, the reference to the new literal is directed to the existing String.

### Why String is immutable ?
In the String constant pool, string object can have one or more references. Several references could point to the same string.
> ***If several references point to same String, it would be bad if one of the references modified that String value. That's why String objects are immutable***

Check below example:
```java
public class StringPoolExample {

    public static void main(String[] args) {
    	//s1,s2 and s3 points to the same string object
        String s1 = "force";
        String s2 = "force";
        String s3 = "force";
		
        System.out.println("s1 == s2 :"+(s1==s2));
        System.out.println("s1 == s3 :"+(s1==s3));
		
	System.out.println("s1 equals s2 :"+(s1.equals(s2)));
        System.out.println("s1 equals s3 :"+(s1.equals(s3)));
    }

}
```
It will not be possible to have a String pool if string objects are not immutable in java.

## Minimizing mutability

Java has many immutable classes, including String, the boxed primitive classes, and BigInteger and BigDecimal. These immutable classes are easier to design, implement and use than mutable classes.
 - Immutable objects are simple: They can be only in one state in which it was created. But mutable objects can have arbitary complex states.
 - Immutable objects are inherently thread-safe; they require no synchronization: They can not be modified by multiple threads since multiple threads only have read-only access to it (no setters available).
 - Immutable objects can be shared freely: Public static final constants  for commonly used values reused wherever possible. Static factories can be used to share instances instead of creating new once. Few examples from java.math.BigInteger.
   - public static final BigInteger ONE − The BigInteger constant one.
   - public static final BigInteger TEN − The BigInteger constant ten.
   - public static final BigInteger ZERO − The BigInteger constant zero.
 - Immutable objects can share their internals as well: negate method in BigInteger class uses the same array which contains the magnitute when creating the new BigInteger. ```java //sample code ```
 - Immutable objects make great building blocks for other objects: Immutable objects make great map keys and set elements. What happens if the keys are mutable? check below code.
 ```java
MyKey key = new MyKey("tic"); //assume hashCode=1234
myHashMap.put(key, "tac");

// Below code will change the key hashCode() and equals()
// but it's location is not changed.
key.setName("toe"); //assume new hashCode=7890

//below will return null, because HashMap will try to look for key
//in the same index as it was stored but since key is mutated,
//there will be no match and it will return null.
myHashMap.get(new MyKey("tic"));
```
 - Immutable objects provide failure atomicity for free: A failed method invocation should leave the object in the state that it was in prior to the invocation. For example, substring(int) method of String class will create a partical copy of the string and return it, instead of changing the original string.
 ```java
String str = "www.harshajayamanna.com";
System.out.println("First 4 char String: " + str.substring(0, 4));
//output : First 4 char String: www.
```
---
> ***Major disadvantage of immutable objects is that they require a seperate object for each operation.***

Creating these objects can be costly. Classes should be immutable unless there's a verry good reason to make them mutable. If a class cannot be made immutable, limit its mutability as much as possible.

Read Effective Java 3 by Joshua Bloch to get more information. I highly recomnend it.

## Reference:
 - https://stackoverflow.com/questions/8798403/string-is-immutable-what-exactly-is-the-meaning
 - https://www.mkyong.com/java/java-mutable-and-immutable-objects/
 - https://docs.oracle.com/javase/tutorial/java/data/strings.html
 - https://webcache.googleusercontent.com/search?q=cache:6yw4ZXFgUDQJ:https://www.baeldung.com/java-thread-safety+&cd=12&hl=en&ct=clnk&gl=sg
 - https://www.oracle.com/technetwork/java/seccodeguide-139067.html#6
 - https://www.amazon.com/Effective-Java-Joshua-Bloch-ebook/dp/B078H61SCH
