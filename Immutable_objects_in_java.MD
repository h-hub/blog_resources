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

## Why String in immutable ?

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



















## Reference:
 - https://stackoverflow.com/questions/8798403/string-is-immutable-what-exactly-is-the-meaning
 - https://www.mkyong.com/java/java-mutable-and-immutable-objects/
