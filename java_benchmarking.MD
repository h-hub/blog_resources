# Java benchmarking  
In computing, a benchmark is the act of running a computer program, a set of programs, or other operations, in order to assess the relative performance of an object, normally by running a number of standard tests and trials against it. Benchmarking in java can be boiled down to measuring how long some operation takes.To measure and find which approach is better, we can write write small benchmark program, often called a **Microbenchmark**. 

Evaluating performance and obtaining metrics of codes in applications, framweworks and tools are essential for developers. but to do that properly, we need to have an understading of how the JVM actually executes Java bytecodes including **dynamic compilation** and **optimization**.
According to 	Brian Goetz, Without understanding the dynamic compilation process, it's almost impossible to correctly write or interpret performance tests for Java classes. Even with that knowledge it is still dificult to write a proper beanchmark program.

## Dynamic compilation and optimization

Java can create "write once, run anywhere" applications.This is achieved by the JVM. Java source code is converted to byte code at the time of compilation and that byte code runs on the JVM.

*javac* is a static compiler.It converts java code into bytecode and does very little optimization
Java is Dynamically compiled. That means, the language is compiled to machine code while the program is being executed, not before. Not much optimizations are done at the time of compilation. JVM constantly tracks what is going on in a Java application and dynamically optimizes accordingly.

#### Just-in-time compilation :time:
JVM has two principal components:the execution engine and the runtime.The execution engine consists of two major components: the garbage collector and the JIT compiler.

Image (https://webcache.googleusercontent.com/search?q=cache:Y0otXQHhWAcJ:https://www.infoq.com/articles/OpenJDK-HotSpot-What-the-JIT+&cd=13&hl=en&ct=clnk&gl=sg)

JIT compilation is an adaptive optimization for methods that are proven to be performance critical. It helps improve the perfomance of the java applications.

#### HotSpots :fire: 
How does JIT works ? At first, it identifies the performace critical methods by maintaining an invocation count. A threshold value (-XX:CompileThreshold) is assgned to the invocation counter at the begining. It is decremented each time the method is called.

Secondly, Once the counter hits zero, JIT is triggered and those methods will be optimized. In this way, codes which are frequently executed and have performance advantages will be optimized. No time will be wasted on infrequent code.

What happened if JIT compiler compiles all the methods ? When JVm starts for the first time. There will be many method calls. Compiling all this could increase the start up time.
In other words, **HotSpot interpreter** analyzes the code as it runs to detect the critical hot spots in the program. It avoids infrequent code(most of the program) and devotes more attention to the performance-critical parts of the program. This hot spot monitoring is continued dynamically as the program runs and adapts its performance on the fly to the user's needs.

#### On-stack replacement (OSR)

In early versions of JVM, HotSpots were identified and compiled and not replaced until the method exited and was re-entered. Compiled version was used only in the next invocation of the method. Sometimes the compiled version was never used in cases such as where all the computation is done in a single invocation of a method.

**OSR** was a solution for this. OSR can swap compiled code with interpreted code(Not optimized) in the middle of a loop/method.
  - How does this work ?
    1. The JVM starts executing some method for the first time ever, in the interpreter, e.g. main().
    2. That method has a long running loop, that is now being executed in the interpreter
    3. The interpreter figures out that the method is hot and triggers a normal compilation
    4. That compilation will be used the NEXT time this method is called, but e.g. it's main() and there is no next time
    5. Eventually the interpreter triggers an OSR compilation.  The OSR is specialized by some bytecode it will be called at, which is typically the loop back-edge branch.
    6. Eventually the OSR compilation completes.
    7. At this point the interpreter jumps to the OSR code when it crosses the specialized entry bytecode – in the middle of the method.

#### Method Inlining

Virtual method invocations is an important optimization bottleneck. What is Virtual method invocations ?? JVM calls the appropriate method for the object that is referred to in each variable. It does not call the method that is defined by the variable's type. 
These method calles require [dynamic dispatching](https://en.wikipedia.org/wiki/Dynamic_dispatch) and that make them much expensive.

Virtual method invocation example:
```java
public class TestBikes {
  public static void main(String[] args){
    Bicycle bike01, bike02, bike03; //Bicycle, MountainBike and RoadBike extend Bicycle class 

    bike01 = new Bicycle();
    bike02 = new MountainBike();
    bike03 = new RoadBike();

    bike01.printDescription(); //A method in Bicycle class will be called
    bike02.printDescription(); //A method in MountainBike class will be called
    bike03.printDescription(); //A method in RoadBike class will be called
  }
}
```
Once JVM has identified hotspots, it performes extensive method inlining together with other optimizations. Benefits of it are,
1. Reduces the dynamic frequency of method invocations and reduce the time it takes for the method invocations.
2. Produces much larger blocks of code for the optimizer to work on. This larger code blocks could lead to even more optimizations.

Method Inlining example:
```java
private int add4(int x1, int x2, int x3, int x4) {
    return add2(x1, x2) + add2(x3, x4);
}
 
private int add2(int x1, int x2) {
    return x1 + x2;
}

//How add4 method would look like after optimization
private int add4(int x1, int x2, int x3, int x4) {
    return x1 + x2 + x3 + x4;
}
```



















## References:
 - https://en.wikipedia.org/wiki/Benchmark_(computing)
 - https://www.ibm.com/developerworks/library/j-jtp12214/#icomments
 - https://www.ibm.com/developerworks/library/j-benchmark1/index.html#artrelatedtopics
 - https://www.oracle.com/technetwork/articles/java/architect-benchmarking-2266277.html
 - https://stackoverflow.com/questions/12600296/dynamically-compiled-language-vs-statically-compiled-language
 - https://www.javaworld.com/article/2078623/core-java-jvm-performance-optimization-part-1-a-jvm-technology-primer.html
 - https://www.javaworld.com/article/2078635/jvm-performance-optimization-part-2-compilers.html
 - https://www.oracle.com/technetwork/java/whitepaper-135217.html#solid
 - https://www.oracle.com/technetwork/articles/java/architect-evans-pt1-2266278.html
 - https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.vm.80.doc/docs/jvm_components.html
 - https://webcache.googleusercontent.com/search?q=cache:ngeOX5sqn24J:https://www.infoq.com/articles/Graal-Java-JIT-Compiler+&cd=1&hl=en&ct=clnk&gl=sg
 - https://webcache.googleusercontent.com/search?q=cache:dls-AEN76T4J:https://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html+&cd=1&hl=en&ct=clnk&gl=sg
 - https://webcache.googleusercontent.com/search?q=cache:Y0otXQHhWAcJ:https://www.infoq.com/articles/OpenJDK-HotSpot-What-the-JIT+&cd=13&hl=en&ct=clnk&gl=sg
 - https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.vm.80.doc/docs/jit_overview.html
 - https://webcache.googleusercontent.com/search?q=cache:mZ8-dPrngZAJ:https://www.h2o.ai/blog/what-the-heck-is-osr-and-why-is-it-bad-or-good/+&cd=1&hl=en&ct=clnk&gl=sg
 - https://dzone.com/articles/how-aggressive-method-inlining
 - https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html
