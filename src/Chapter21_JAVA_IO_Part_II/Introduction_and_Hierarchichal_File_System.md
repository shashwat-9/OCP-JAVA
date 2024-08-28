## Introduction
 - The standard I/O package is good with writing data into files. But for managing files and directories in a file system
, java.nio package(NIO.2, Non-blocking Input/Output version 2) provides enhanced and newer alternatives.
 - NIO.2 helps in accessing files, managing attributes and traversing the file systems.
 - Primary support for file I/O and accessing files and directories in a file system is provided by the java.nio.file package. 
 - Both I/O APIs are inter-operable

## Characteristics of a Hierarchical File System

### Hierarchical File System
 - A file system allows persistent storage and organization of data as a hierarchical (or tree) structure on some external
media. The hierarchy is always tree-like structure.
 - An operative system can have multiple file systems, each of which is identifiable by its root component.
 - Root-component is platform dependent. On unix based system, the root component is '/' and on windows-based system it 
starts with the volume name(C, D) and then ":\".
 - Each directory/file is uniquely identifiable by its path from root component.
 - The name(name elements in path) separator character on unix-based is '/' and on windows-based system is '\'.
```
    //Both have 3 name elements
    /a/b/c           on Unix-based platforms
    C:\a\b\c         on Windows-based platforms

```

##### Absolute and Relative Paths
 - An absolute path starts with the platform dependent root component and uniquely identifies the directory/file on a file
system.
 - A relative path is without the root component and requires additional information to locate it on a file system, and 
is in relation to the current directory.
 - File extensions can be used to distinguish a filename from a directory but is immaterial to the file system.
 - The current directory is designated by a period character '.' and the parent directory '..'

##### Symbolic Links
 - A symbolic link(also called a hard link, shortcut or alias) is a special file that acts as a reference to another file
/directory called target of the symbolic link.
 - Deleting the symbolic link doesn't delete the target file.
 - In many file operations, it is possible to indicate whether symbolic links should be followed or not.
