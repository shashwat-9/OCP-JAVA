# Program

 - Source code that is compiled and run.

## Compiling

 - JDK provides tools for compiling and running java programs.
 - Classes in Java SE Platform API are already compiled, JDK knows how to find them.
 - Java source files are compiled using java compiler __javac__.
 - Each class declaration in source file(.java) is compiled into a separate class file(.class)
containing its java bytecode.
 - The name of the compiled file is classname.class
 - A java file can contain multiple class declarations, though at most one class can have public access.
 - If a class declaration have public access in a file, then the file should be named as the classname.java where 
classname is the public class in the source file.

#### To compile multiple file using a single cmd

```
> javac file1.java file2.java file3.java ...
```

## Running

 - A java program is run by Java Application Launcher, java - which is a cmd.
 - java cmd creates an instance of JVM that executes the bytecode.

```
> java TestFile
```

