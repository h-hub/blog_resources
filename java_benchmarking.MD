# Java benchmarking  
In computing, a benchmark is the act of running a computer program, a set of programs, or other operations, in order to assess the relative performance of an object, normally by running a number of standard tests and trials against it. Benchmarking in java can be boiled down to measuring how long some operation takes.To measure and find which approach is better, we can write write small benchmark program, often called a **Microbenchmark**. 

Evaluating performance and obtaining metrics of codes in applications, framweworks and tools are essential for developers. but to do that properly, we need to have an understading of how the JVM actually executes Java bytecodes including **dynamic compilation** and **optimization**.
According to 	Brian Goetz, Without understanding the dynamic compilation process, it's almost impossible to correctly write or interpret performance tests for Java classes. Even with that knowledge it is still dificult to write a proper beanchmark program.

## Dynamic compilation and optimization

Java can create "write once, run anywhere" applications.This is achieved by the JVM. Java source code is converted to byte code at the time of compilation and that byte code runs on the JVM.

Java is Dynamically compiled. That means, the language is compiled to machine code while the program is being executed, not before. Not much optimizations are done at the time of compilation. JVM constantly tracks what is going on in a Java application and dynamically optimizes accordingly.

#### Just-in-time compilation

















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
