## Classes in Java
A class is the blueprint from which individual objects are created. In object-oriented terms, we say that your bicycle, his bicycle and her bicycle are instances of the class of objects known as bicycles

below is the the bicycle class.
```java
class Bicycle {

    int cadence = 0;
    int speed = 0;
    int gear = 1;

    void changeCadence(int newValue) {
         cadence = newValue;
    }

    void changeGear(int newValue) {
         gear = newValue;
    }

    void speedUp(int increment) {
         speed = speed + increment;   
    }

    void applyBrakes(int decrement) {
         speed = speed - decrement;
    }

    void printStates() {
         System.out.println("cadence:" +
             cadence + " speed:" + 
             speed + " gear:" + gear);
    }
}
```
More about classes can be found here https://docs.oracle.com/javase/tutorial/java/javaOO/index.html

## Nested Classes
Java allows you to define a class within another class.As a member of the OuterClass, a nested class can be declared private, public, protected, or package private. 
There are two types of nested classes.

1. Static nested classes: They do not have access to other members of the enclosing class. A static nested class cannot refer directly to instance variables or methods defined in its enclosing class: it can use them only through an object reference. 
```java
/Example
public class Outer {

	private static int number = 10;
	private String name = "danny";

	static class NestedStatic {
	  public void myMethod() {
	  
		 System.out.println("This is my nested class");
		 System.out.println(number);
		 
		 //Can access instance variables of the outer class
		 //only through an object reference
		 Outer outer = new Outer();
		 System.out.println(outer.name);
	  }
	}

	public static void main(String args[]) {
	  Outer.NestedStatic nested = new Outer.NestedStatic();	 
	  nested.myMethod();
	}
}
```
2. Non-static nested classes (inner classes): They have access to other members of the enclosing class, even if they are declared private.

```java
//how nested classes are declared.
class OuterClass {
    ...
    static class StaticNestedClass {
        ...
    }
    class InnerClass {
        ...
    }
}
```
### Why Use Nested Classes ?
1. **logically grouping classes that are only used in one place.** The Map interface in java provides a small nested interface called Map.Entry, the type of the elements in this Set. Since the entry interface will only be used by the map interface, it is logical to keep it as a nested interface. Entry object cannot exist without a map(https://docs.oracle.com/javase/tutorial/collections/interfaces/map.html). Set<Map.Entry<K,V>> entrySet() : Returns a Set view of the mappings contained in this map. This set contains Map.Entry objects (
https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#entrySet--)

```java
//Example:
import java.util.*;
public class HashExample {

   public static void main(String args[]) {
      // Create a hash map
      Map<String, Integer> map = new HashMap<String, Integer>();

      // Put elements to the map
      map.put("martin", 1);
      map.put("kent", 2);
      map.put("grady", 3);
      map.put("bob", 4);
      
      // Get a set of the entries
      Set set = map.entrySet();
      
      // Get an iterator
      Iterator i = set.iterator();
     
      // Display elements 
      while(i.hasNext()) {
         Map.Entry me = (Map.Entry)i.next();
         System.out.print(me.getKey() + ": ");
         System.out.println(me.getValue());
      }
      System.out.println();
   }
}
```
2. **Increases encapsulation:** Inner classes are scoped to the class used to declare them -- thus they are effectively "invisible" to the other classes in the same package.
3. **More readable and maintainable code:** It enables the developer to create a set of classes within a containing class without cluttering up the name space of classes in their package.
 

## Anonymous Classes
They enable you to declare and instantiate a class at the same time.

References:
https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html
https://www.javaworld.com/article/2077044/a-look-at-inner-classes.html
