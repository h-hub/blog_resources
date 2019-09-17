# Java 13 is here

java 13 will generaly be available from 2019/09/17. This is the second java release for this year followed by java 12. java release schedule was changed in 2017 and now we get 2 java releases per year. It has its advantages.

We know that java 8 was a major release which shipped fatures such labmda expression. My personal interset for java grown after that an di believe there are many other who share my thoughts.

## Features of JDK 13

Java 13 brings several enhansments to the Java world.

## 1. JEP 350 – Dynamic CDS Archives
First of all, What is CDS (Class Data Sharing) : It helps reduce the startup time and memory footprint between multiple Java Virtual Machines (JVM).
By using the JRE installer or by manually, you can a create representation of default set of classes from the system Java Archive (JAR) in file called  shared archive.
If you have several java application running, read-only JVM metadata can be shared among the applications. This done by memory-mapping the shared archive. Shared archive is faster than loading the classes.
Application Class-Data Sharing (ApsCDS) is an extension of CDS which enables application classes to be placed in a shared drive and share common class metadata among java processes. To enable this we have to create a class list for each application
Goal of JEP 350 is to eliminate the need create a class list for each application and allow the dynamic archiving of classes at the end of Java application execution.

## 2. JEP 351 – ZGC: Uncommit Unused Memory:
The Z Garbage Collector(ZGC) is a scalable low latency garbage collector. It is a concurrent garbage collector, meaning all heavy lifting work is done while Java threads continue to execute. Goals of ZGC are,
 - Pause times do not exceed 10ms.
 - Pause times do not increase with the heap or live-set size.
 - Handle heaps ranging from a few hundred megabytes to multi terabytes in size.
 
Goal of JEP 351 – ZGC: Uncommit Unused Memory is to Enhance ZGC to return unused heap memory to the operating system. This usefull in cases such as Container environments where memory footprint is a concern and resources are paid by use.

## 3. JEP 353 – Reimplement the Legacy Socket API:
Java Sockets are being used to implement application which requires reliable and lower-level network communication. Operation such sending database query results to client applications and sending stock prices to the users are examples.
Goal of JEP 353 is to replace the current implementation of java.net.Socket and java.net.ServerSocket APIs. The new APi is simpler, moderns, easy ti bebug and maintain.

## 4. JEP 354 – Switch Expressions (Preview):
Extend switch so it can be used as either a statement or an expression.
### Arrow labels
New simplified form, with 'case L ->' labels. If a label is matched, then only the expression or statement to the right of the arrow is executed; there is no fall through.
```java
static void howMany(int k) {
    switch (k) {
        case 1  -> System.out.println("one");
        case 2  -> System.out.println("two");
        default -> System.out.println("many");
    }
}
```

The following code:
```java
howMany(1);
howMany(2);
howMany(3);
```

results in the following output:
```java
one
two
many
```
### Switch expressions
Switch statement can be used as an expression.
```java
static void howMany(int k) {
    System.out.println(
        switch (k) {
            case  1 -> "one"
            case  2 -> "two"
            default -> "many"
        }
    );
}
```
### Yielding a value
A new yield statement to yield a value, which becomes the value of the enclosing switch expression.
```java
int j = switch (day) {
    case MONDAY  -> 0;
    case TUESDAY -> 1;
    default      -> {
        int k = day.toString().length();
        int result = f(k);
        yield result;
    }
};
```
### Exhaustiveness
The cases of a switch expression must be exhaustive; for all possible values there must be a matching switch label. That means the default clause is required. Moreover, a switch expression must either complete normally with a value, or complete abruptly by throwing an exception.
```java
int i = switch (day) {
    case MONDAY -> {
        System.out.println("Monday"); 
        // ERROR! Block doesn't contain a yield statement
    }
    default -> 1;
};
i = switch (day) {
    case MONDAY, TUESDAY, WEDNESDAY: 
        yield 0;
    default: 
        System.out.println("Second half of the week");
        // ERROR! Group doesn't contain a yield statement
};
```

Also, the control statements, `break`, `yield`, `return` and `continue`, cannot jump through a switch expression
```java
for (int i = 0; i < MAX_VALUE; ++i) {
        int k = switch (e) { 
            case 0:  
                yield 1;
            case 1:
                yield 2;
            default: 
                continue z; 
                // ERROR! Illegal jump through a switch expression 
        };
    ...
    }
 ```
## JEP 355 – Text Blocks (Preview):
A text block is a multi-line string literal that avoids the need for most escape sequences, automatically formats the string in a predictable way. This would embedding a snippet of HTML, XML, SQL, or JSON in a string literal "..." easy.
```java
String html = """
              <html>
                  <body>
                      <p>Hello, world</p>
                  </body>
              </html>
              """;
 ```
 The content of a text block is processed by the Java compiler in three distinct steps


I have summarized the features of JDK 13 and for more information please follow the links in the Reference section.

# References:
 - https://docs.oracle.com/javase/10/vm/class-data-sharing.htm#JSJVM-GUID-2942983A-E83C-4DA3-A60C-60411D731D5A
 - https://docs.oracle.com/javase/10/tools/java.htm#JSWOR-GUID-EE6BD9FA-EF6D-4C3E-AC5C-30B8762CDC1B
 - https://openjdk.java.net/jeps/350
 - https://wiki.openjdk.java.net/display/zgc/Main
 - https://openjdk.java.net/jeps/351
 - https://openjdk.java.net/jeps/354
 - https://docs.oracle.com/javase/tutorial/networking/sockets/index.html
 - https://openjdk.java.net/jeps/353
 - https://openjdk.java.net/jeps/355
