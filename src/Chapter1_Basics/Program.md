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
> java ClassFile
```

 - ClassFile is the class name of the starting point of program, containing the main method.
 - Typically, a source code is compiled using javac and then class file is run using java cmd.
 - But if the entire source code is contained in one file, we can omit the compilation and run the code in memory.
 - If all the required classes are in one java file, then the java program can be run using :
```
java Prg.java
```

##### In order to run a single-file source-code program, the following conditions must be met:

 - The single source file must contain all source code for the program.

 - Although there can be several class declarations in the source file, the first class declaration in 
the source file must provide the main() method; that is, it must be the entry point of the program.

 - There must not exist class files corresponding to the class declarations in the single source file that are 
accessible by the java command.

 - Unlike the javac command, the name of the single source file (e.g., Demo-App.java) need not be a valid class name, 
but it must have the .java extension. Also unlike the javac command, the java command allows several public classes 
in the single source file (only public classes in the Demo-App.java file).

```
// File: Demo-App.java
public class TestPoint3D {
  // Implementation
  // Provides the main() method and is the first class declaration in the file.
}

public class Point2D {
  // Implementation
}

public class Point3D extends Point2D {
  // Implementation
}
```

