# Operations On Directory Entries
 - static methods of Files class access directory entries in a file system.

### Characteristics of Methods in the Files Class
 - Resources like files, streams etc should be closed after usage. All of these resources implements java.io.Closeable 
interface, which is best handled with try-with-resources statement.

#### Handling Exceptions
 - Errors are bound to occur, and among the most common errors, IOException and permission to access a file are common 
Exception.
 - IOException has a subclass called java.nio.file.NoSuchFile-Exception, which makes the cause obvious.

#### Handling Symbolic Links
 - The methods of Files, have a variable arity parameter, wherein we may pass a parameter called LinkOption.NOFOLLOW_LINKS
which specify not to follow the symlinks.

#### Executing Atomic Operations
 - Certain resources can be utilised atomically, thereby guarantees the integrity of resource and can't be utilised by 
any other concurrent operations.

#### Determining the Existence of a Directory Entry
```
    static boolean exists(Path path, LinkOption... options)
    static boolean notExists(Path path, LinkOption... options)
```
 - These method whether the files exist or not at a given location.
 - Both returns false if they're not able to __determine__ whether a directory exists or not.

#### Uniqueness of directory entry
```
    static boolean isSameFile(Path path1, Path path2) throws IOException
```
 - This method checks whether two paths denotes the same directory entry or not.
 - This method doesn't check whether the path exists or not.
 - This method normalizes the paths and follows symbolic links.
 - It implements an equivalence relation(reflexive, symmetric, transitive)

#### Deleting Directory Entries
```
    static void delete(Path path) throws IOException
    static boolean deleteIfExists(Path path) throws IOException
```
 - Deleting a symbolic link only deletes the link, and not the target of the link.
 - To delete a directory, it must be empty or a java.nio.file.DirectoryNotEmpty-Exception is thrown.
 - Also keep in mind that deleting a directory entry might not be possible, if another program is using it.

#### Copy Options
 - The enum type LinkOption and StandardCopyOption implements CopyOption interface.
 - A variable arity parameter of type CopyOption... is declared by the copy() and move() methods of the Files class that
support specific constants of the LinkOption and StandardCopyOption enum types.
 - The values of java.nio.file.StandardCopyOption are :
1. __REPLACE_EXISTING__ - Replaces a file if it exists
2. __COPY_ATTRIBUTES__ - copy file attributes to a new file
3. __ATOMIC_MOVE__ - Move the file as an atomic file system operations. Meaning it is uninterrupted during its execution

#### Copying Directory Entries
```
    static Path copy(Path source, Path destination, CopyOption... options)
                throws IOException
```
 - returns the path of destination directory entry. The default behaviour is outlined as below but these can be configured 
using copy option :
1. If a destination already exists or is a symlink, copying fails.
2. If source and destination are the same, the method completes without any copying.
3. If source is a symbolic link, the target of the link is copied.
4. If source is a directory, just an empty destination directory is created.

The following options can be specified to configure the default copying behaviour :
1. __StandardCopyOption.REPLACE_EXISTING__: If the destination exists, this option indicates to replace the destination if 
it is a file or an empty directory. If the destination exists and is a symbolic link, it indicates to replace the symbolic
link and not its target.
2. __StandardCopyOption.COPY_ATTRIBUTES__: This option indicates to copy the file attributes of the source to the destination.
However, copying of attributes is platform dependent.
3. __LinkOption.NOFOLLOW_LINKS__: This option indicates not to follow symbolic links. If the source is a symbolic link, 
then the symbolic link is copied and not its target.
```
    static long copy(InputStream in, Path destination, CopyOption... options)
                    throws IOException
```
 - Returns the number of bytes copied. The input stream will be at the end of the stream after copying, but may not be 
because of I/O errors.
 - By default, if the destination path already exists or is a symbolic link, copying fails.
```
    static long copy(Path source, OutputStream output) throws IOException
```
 - Copies all bytes from the source to the output stream, and returns the number of bytes copied. It may be necessary to
flush the output stream.
 - The copy method doesn't create a path, if the parent path doesn't exist, NoSuchFileException is thrown.
 - The copy method doesn't copy the entries in a source directory to a destination directory. If such an attempt is made
then either an empty directory will be created(even if a directory or a file already exists with the same name) or if the
destination directory exists, then DirectoryNotEmptyException will be thrown.
 - In cases where the path represents a file, a new file is created and the contents are copied to this file, or a replacing
file is created, if the name exists at the destination as a directory, then if empty it is deleted a new file is created
with the same contents. Else if the directory is non-empty, then DirectoryNotEmptyException is thrown.
