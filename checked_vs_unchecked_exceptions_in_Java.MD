# Checked vs Unchecked Exceptions: The Controversy

> Definition: An exception is an event, which occurs during the execution of a program, that disrupts the normal flow of the program's instructions.

## What are checked exception ?
Exceptional conditions that a well-written application should anticipate and recover from. Example: User supplies the name of a nonexistent file. In this case,  A well-written program should catch this exception and notify the user of the mistake.
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class FileReadExample {

    public static void main(String[] args) {

        StringBuilder sb = new StringBuilder();

        try (BufferedReader br = Files.newBufferedReader(Paths.get(args[0]))) {

            // read line by line
            String line;
            while ((line = br.readLine()) != null) {
                sb.append(line).append("\n");
            }

        } catch (IOException e) {
            System.err.format("IOException: %s%n", e);
        }

        System.out.println(sb);

    }

}
// How to run : java FileReadExample.java file.txt
```
## Whar are errors ?
These are exceptional conditions that are external and cannot be recovered from. Example:  An application is unable to read the file because of a hardware or system malfunction. In this case it is makes sence to print a stack trace and exit

## What are RuntimeException ?
These are exceptional conditions that are internal to the application, and that the application usually cannot anticipate or recover from.
> RuntimeExceptions occur due to programming bugs, such as logic errors or improper use of an API.

Example: If a logic error causes a null to be passed to the constructor which does not accepts null values, the constructor will throw NullPointerException. Runtime exceptions are not subject to the Catch or Specify Requirement. You must not catch or handle RuntimeExceptions.

RuntimeExceptions send output to System.err. We can configure log4j to log the System.err output properly. This enables us to identify and fix bugs/errors in the code.

https://www.mkyong.com/logging/log4j-log4j-properties-examples/

---

> All exceptions are checked exceptions, except for those indicated by Error, RuntimeException, and their subclasses.

> Runtime exceptions are those indicated by RuntimeException and its subclasses.


## What is the Controversy ?

**According to Oracle:** You should not write code which throws only unchecked exceptions or make all exceptions inherit from RuntimeException, eventhough Java does not require methods to catch or to specify unchecked exceptions. If you do this, you will be ignoring the catch or specify requirement and could cause problem to the users of your class.
 
Any Exception that can be thrown by a method (we throw only checked expcetion) is part of the method's public programming interface. Users of the method should know about these exception inorder for them to choose what to with those.

Why shouldn't you Specify or throw Runtime exceptions in a method ?  Runtime exceptions represent problems that are the result of a programming problem. Users of the class wonnt be able to recover from it.Runtime exceptions could occur anywhere and there can be many. Specifying Runtime exceptions in a method could reduce the clarity.

The summary is: If a client can reasonably be expected to recover from an exception, make it a checked exception. If a client cannot do anything to recover from the exception, make it an unchecked exception.

**According to Brian Goetz:** In an IBM article, firstly, Brian mentioned the same thing that was in the oracle website and also he has pointed out few items from the *Effective Java: Programming Language Guide*.I'll smmarize his what he has said in the next few paragraphs.

Bruce Eckel and Rod Johnson have concluded that exclusive use of checked exceptions is not a good idea. While Eckel suggests all exceptions should be unchecked, Rod Johnson suggests the orthodox preference for checked exceptions is excessive. They point out the properties, implementation and widespread misuse of checked exceptions.

He has shared some of the critisms of Checked exceptions,

Exposing the implementation details inappropriately: Here he talks how Exception chaining can be used to throw a more appropriate exception. Developers throw the details of the underlying failure without throwinf any meaningfull exception which could explain the implementation and what has gone wrong. An example would be throwing `SQLException` when you can throw `NoSuchUserException` which could explain what exactly gone wrong. 
```java
//example code
```

Unstable method signatures: 


## References:
- https://docs.oracle.com/javase/tutorial/essential/exceptions/definition.html
- https://www.javaworld.com/article/3142626/are-checked-exceptions-good-or-bad.html?page=2
- https://stackoverflow.com/questions/613954/the-case-against-checked-exceptions
- https://www.ibm.com/developerworks/library/j-jtp05254/index.html
- http://webcache.googleusercontent.com/search?q=cache:lsZlKrJdRwkJ:briangoetz.blogspot.com/2007/06/remove-checked-exceptions.html+&cd=15&hl=en&ct=clnk&gl=sg
- https://webcache.googleusercontent.com/search?q=cache:z_D9XOwyUTMJ:https://www.theserverside.com/discussions/thread/21538.html+&cd=18&hl=en&ct=clnk&gl=sg
- https://webcache.googleusercontent.com/search?q=cache:UazO-1DUo0QJ:https://www.artima.com/intv/solid.html+&cd=1&hl=en&ct=clnk&gl=sg
