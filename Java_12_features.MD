# What's new in Java 12 (OpenJDK)?

## 1. Shenandoah: A Low-Pause-Time Garbage Collector (Experimental)
A GC algothim which aimns to reduce the GC paus time regarless of the heap size. Evacuation work will be done concurrently with the running Java threads.
Shenandoah is an appropriate algorithm for applications which value responsiveness and predictable short pauses. For most applications, it is important to meet SLAs and operate without issues using the given resources (Memory, CPU, ..). Not interupting the running program is essential to achieve this.Shenandoah has been implemented by Red Hat. Shenandoah is different from the currently available GCs in JDK.
### Links:
 - https://webcache.googleusercontent.com/search?q=cache:PpGaKYsoxxgJ:https://openjdk.java.net/jeps/189+&cd=1&hl=en&ct=clnk&gl=sg
 - https://www.researchgate.net/publication/306112816_Shenandoah_An_open-source_concurrent_compacting_garbage_collector_for_OpenJDK

## 2. Microbenchmark Suite


























## References
 - https://webcache.googleusercontent.com/search?q=cache:6DF6DpesS0gJ:https://www.infoq.com/presentations/jmh+&cd=12&hl=en&ct=clnk&gl=sg
 - https://www.oracle.com/technetwork/articles/java/architect-benchmarking-2266277.html
 - https://webcache.googleusercontent.com/search?q=cache:n9lB93qMNFkJ:https://www.azul.com/presentation/the-art-of-java-benchmarking/+&cd=13&hl=en&ct=clnk&gl=sg
 - https://www.ibm.com/developerworks/library/j-benchmark1/index.html
