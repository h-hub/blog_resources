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

 - According to Oracle: You should not write code which throws only unchecked exceptions, eventhough Java does not require methods to catch or to specify unchecked exceptions. 


## References:
- https://docs.oracle.com/javase/tutorial/essential/exceptions/definition.html
- https://www.javaworld.com/article/3142626/are-checked-exceptions-good-or-bad.html?page=2
- https://stackoverflow.com/questions/613954/the-case-against-checked-exceptions
