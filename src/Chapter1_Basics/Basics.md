# BASICS
Java SE 17 version is available as LTS(Long Term Support).

## Java Platforms

1. Java SE - Core Functionality, targets Desktop and server applications.
2. Java EE - Extension of Java SE, targets Enterprise Grade Application.
3. Java ME - Micro Edition, subset of SE, targets systems like set-top box, embedded systems.
4. Java Card - Smaller version of all, targets smart cards and alikes.

 - Each platform provides a hardware/OS specific JVM.
 - Java program developed for one Java platform will not necessarily run under the JVM of another Java platform. 
The JVM must be compatible with the Java platform that was used to develop the application.
 - APIs and runtime support is provided within JDK for java.
 - Starting from java 11, JRE is not a separate module rather included in JDK.
 - Jlink is a tool in within jdk, used to create runtime images.

## Multi-paradigm

1. Java is an object-oriented programing Language.
2. It Works in Procedural Paradigm as well.
3. Evolved to support Function Programming Paradigm(lambda, Functional Interface).

## JVM

1. Java Programs compiles to bytecode, that is executed over JVM.
2. Other languages such as Scala, Groovy, and Clojure, now compile to bytecode and seamlessly execute on the JVM.
3. Available for every OS/Hardware and thus makes bytecode architecture neutral.
4. JVM can load/link class libraries at runtime dynamically.

## Reliable, Robust and Secure

1. Garbage Collection, Runtime Index check for arrays and String promotes Reliability
2. Exception handling promotes Robustness of Systems developed in java.
3. Java Security model provides security from un-trusted code in java which are unsafe. JVM provides multi-level 
protection form malicious code execution and limit the execution of malicious code.

## High Performance and MultiThreading

1. JVM has many features to optimize the java bytecode at runtime like JIT, optimizing the performance critical
bytecode(hotspot).
2. Java Provides multiThreading to utilize the multicore architecture. Functional programming is also aiding in 
utilizing the same. 