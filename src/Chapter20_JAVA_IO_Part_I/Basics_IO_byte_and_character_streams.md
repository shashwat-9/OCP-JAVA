# Java SE 17

## Java I/O Part I
 - java.io & java.nio packages provide function that deals with I/O to various destinations.
 - read/writes various kind of data : bytes, characters, binary files, text files, buffered I/O, Object Serialization.
 - It also provides access to file systems.

### Input and Output
 - I/O streams implement sequential processing of data.
 - The following entities can act as both input and output streams:
    1. File
    2. Array of bytes or characters
    3. A network connection

 - Two categories of I/O streams :
    1. Byte Streams
    2. Character streams

 - A low level I/O stream operates directly on the data source(file, array of bytes) process the data as bytes.
 - A high level I/O is chained to an underlying stream and provides additional capabilities. It is basically a wrapper
to an underlying low level I/O stream. For e.g., processing the bytes from the stream as int or another java primitive.

 - The abstract classes InputStream and OutputStream are the root of the inheritance for all the classes that perform
byte reading/writing.
 - InputStream have the following methods:
   1. int read() throws IOException
   2. int read(byte[] b) throws IOException
   3. int read(byte[] b, int off, int len) throws IOException

 - The read method reads a single byte, and returns an int value. The byte lies in the least significant 8 bits.
 - (-1) is the return value when the input stream reached the end.
   ```
      long transferTo(OutputStream out) throws IOException
   ```
 - transfers the inputStream to the specified outputStream.
 - OutputStream abstract class have the following methods :
   1. void write(int b) throws IOException
   2. void write(byte[] b) throws IOException
   3. void write(byte[] b, int off, int len) throws IOException

   - The first method takes int as the parameter and is truncated to the least eight significant bits for byte writing .
   ```
      void close() throws IOException -- Both InputStream and OutputStream
      void flush() throws IOEXception -- Only for OutputStream  
   ```
   - An I/O stream should be closed when no longer needed, to free system resources. Closing an outputStream flushes out
the buffer automatically.
   - ByteStream implements AutoCloseable interface, and thus can be declared with try-with-resources statement.
   - Read and write operations on streams are blocking operations - they don't return until the operation is completed.
   - Many methods in java.io package throws checked IOException. A calling method therefore must catch or throws.

![ByteStreamHierarchy](/Resources/ByteStreamHierarchy.jpg)
#### File Streams
FileInputStream and FileOutputStream are low-level stream that are connected to files.

```
//constructors

    FileInputStream(String name) throws FileNotFoundException

    FileOutputStream(String name) throws FileNotFoundException
    FileOutputStream(String name, boolean append) throws FileNotFoundException
```

 - If the file does not exist, a FileNotFoundException is thrown. If it exists, it is set to be read from beginning.
 - If the file does not exist in the latter case, it is created. If it exists, its contents are reset, unless appropriate
constructor is used to indicate that output should be appended to the file. A SecurityException is thrown if the file
does not have the write access, or it cannot be created. A FileNotFoundException is thrown if it's not possible to open
the file for any other reason.

#### I/O Filter Streams
An I/O filter stream manipulates the raw data from the underlying stream in some way and provides some additional 
functionalities.

 - FilterInputStream and FilterOutputStream together with its subclasses define input and output FILTER streams.
 - The BufferedInputStream and BufferedOutputStream implement filter streams that buffer input from and output to the
underlying stream, respectively.
 - The subclasses DataInputStream and DataOutputStream implement filter streams that allow binary representation of Java
primitive values to be read and written, respectively, from and to an underlying stream.

##### Reading and Writing Binary Values
To allow reading/writing of binary representation of java primitives, streams can implement DataInput/DataOutput interface.
 - The method for writing/reading binary representation of java primitives is readX/writeX, where X is the java primitive
or String or UTF.
 - A file containing binary values(i.e., binary representation of java primitive values) is called a binary file.
 - The recommended practice for reading and writing characters is to use character stream called reader and writers.
 - In addition to IOException, the read method also throws __EOFException__, when the inputStream doesn't contain the correct
no of bytes to read.
 - Bytes can also be skipped from a DataInput stream, using the skipBytes(int n) method which skips n bytes.
 - Read the (exact number of) Java Primitive values in the same order they were written out to the file, using relevant 
readX() methods. Not doing so will unleash the wrath of the IOException.
 - Use a try-with-resources statement for declaring and creating the necessary streams, which guarantees closing of filterStream
or any underlying stream.
 - The int argument in the writeX method is converted to the corresponding type before writing.

###### Summary
1. The Byte Streams writes a single byte at a time.
2. If using DataInputStream to read and write, there should be required bytes of the particular type and the returned 
value will be the concatenation of the bytes written thereof.

##### Character Streams
 - A character encoding is a scheme for representing characters.
 - Java Programs represent values of the char type internally in the 16-bit Unicode character encoding, but the host
platform might use another character encoding to represent and store characters externally.
 - The abstract classes Reader and Writers are the roots of the inheritance hierarchies for streams that read and write 
Unicode characters using a specific character encoding.
 - A reader is an input character stream that implements the Readable interface and reads a sequence of unicode characters
, and a writer is an output character stream that implements the Writer interface and writes a sequence of unicode characters.
 - Character encodings (usually called charsets) are used by readers and writers to convert between external bytes and 
internal Unicode characters.
 - The same character encoding that was used to write the characters must be used to read those characters.
 - The java.nio.charset.Charset class represents charsets.

![CharacterStream](/Resources/CharacterStreamHierarchy.jpg)

```
   static Charset forName(String charsetName)
```
 - Returns a charset object for teh named charset. Selected common charset names are "UTF-8", "UTF-16", "US-ASCII" and "ISO-8859-1".
```
   static Charset defaultCharset()
```
 - Returns the default charset of the Java virtual machine.
```
   int read() throws IOException
   int read(char cbuf[]) throws IOException
   int read(char cbuf[], int off, int len) throws IOException
```
- Readers and Writers require underlying inputStream and outputStream.
```
   long skip(long n) throws IOException
```
 - A reader can skip over characters using the skip() method.
```
   void close() throws IOException
```
 - To close the stream
```
   boolean ready() throws IOException
```
 - When called,this method returns true if the next read operation is guaranteed not to block. Returning false does not
guarantee that the next read operation will block.
 - Writers use the following methods for writing Unicode characters.
```
   void write(int c) throws IOException
```
 - The write() method takes int as an argument, but writes only the least significant 16 bits.
```
   void write(char[] cbuf) throws IOException
   void write(String str) throws IOException
   void write(char[] cbuf, int off, int length) throws IOException
   void write(String str, int off, int length) throws IOException
```
 - Write the characters from an array of characters or a string.
```
   void close() throws IOException
   void flush() throws IOException
```
 - Like byte streams, a character stream should be closed when no longer needed in order to free system resources. Closing
a character output stream automatically flushes the stream. A character output stream can also be manually flushed.
 - Many methods of character stream throws IOException.
 - They also implement AutoCloseable interface.

##### PrintWriter
 - PrintWriter is used to write a text representation. It should be chained to a writer or a byte output stream.
```
   PrintWriter(Writer out)
   PrintWriter(Writer out, boolean autoFlush)
   PrintWriter(OutputStream out)
   PrintWriter(OutputStream out, boolean autoFlush)
   PrintWriter(String fileName)
   PrintWriter(String fileName, Charset charset) throws FileNotFoundException
   PrintWriter(String fileName, String charsetName) throws FileNotFoundException, UnsupportedEncodingException
```
 - The boolean autoFlush argument specifies whether the PrintWriter should do automatic line flushing when println() or
printf() method are called.

 - When the underlying writer is specified, the character encoding supplied by the underlying writer is used. However, an
OutputStream has no notion of any Character encoding, so the necessary intermediate OutputStreamWriter is automatically
created, which will convert characters into bytes, using the default character encoding.
```
   boolean checkError()
   protected void clearError()
```
 - The first method flushes the output stream if it's not closed and checks its error state.
 - The second method clears the error state of this output stream.

##### Writing Text Representation of Primitive Values and objects
 - The println() methods write the text representation of their argument to the underlying stream, and then append a line
separator. The println() method uses the correct platform-dependent line separator.
 - The print methods create a text representation of an object by calling the toString() method on the object. The print
methods do not throw any IOException. Instead, the checkError() method of the PrintWriter class must be called to check
for errors.

##### Writing formatted Values
 - PrintWriter provides two methods, format() and printf().
```
   PrintWriter format(String format, Object.., args)
   PrintWriter format(Locale loc, String format, Object... args)
   PrintWriter printf(String format, Object... args)
   PrintWriter printf(Locale loc, String format, Object... args)
```
 - Any error in the format string will result in a runtime exception.

##### Writing Text Files
 - For Writing text representation of a values to file using default character encoding, any of the following procedures
can be used:
```
   1. Object of Class PrintWriter -> Object of Class OutputStreamWriter -> Object of Class FileOutputStream
   //The OutputStreamWriter uses the default character encoding
   PrintWriter pw1 = new PrintWriter(new OutputStreamWriter(new FileOutputStream("fileName.txt")));

   2. Object of class PrintWriter -> Object of Class FileOutputStream 
   // The intermediate OutputStreamWriter to convert the characters
   PrintWriter pw2 = new PrintWriter(new FileOutputStream("fileName.txt"));
   
   3. Object of Class PrintWriter -> Object of class FileWriter 
   // true value for the argument autoflush is used to flush the output buffer by the methods println() and printf() methods.
   FileWriter fw = new File("fileName.txt") -> this statement is equivalent to having an OutputStreamWriter chained to a 
   FileOutputStream.
   PrintWriter pw3 = new PrintWriter(new FileWriter("fileName.txt"));
   
   4. PrintWriter pw4 = new PrintWriter("fileName.txt");
   //The underlying OutputStreamWriter is created to write the characters to the file in default encoding. In this case,
   there is no automatic flushing by println() and printf() methods.
```
 - If a specific character encoding is desired for the writer, the third procedure can be used, with the encoding being
specified for the FileWriter:
```
   Charset utf8 = Charset.forName("UTF-8");
   FileWriter fileWriter = new FileWriter("info.txt", utf8);
   PrintWriter printWriter5 = new PrintWriter(fileWriter, true);
```
 - This writer will use the UTF-8 character encoding to write the characters to the file. Alternatively, we can use a
PrintWriter constructor that accepts a character encoding:
```
   Charset utf8 = Charset.forName("UTF-8");
   PrintWriter printWriter6 = new PrintWriter("info.txt", utf8);
```

 - A BufferedWriter can also be used to improve the efficiency of writing characters to the underlying stream, as explained
later.

##### Reading Text Files
 - When reading characters from a file using the default character encoding, the following two procedure for setting up
an InputStreamReader can be used.
```
1.
   FileInputStream inputFile = new FileInputStream("fileName.txt");
   InputStreamReader reader = new InputStreamReader("inputFile);
   //The inputStream uses a default character encoding for the reading the characters from the file.

2. 
   FileReader fileReader = new FileReader("info.txt");
   // This is equivalent to having an InputStreamReader chained to a FileInputStream for reading the characters from the
file, using the default character encoding.
```
 - If a specific character encoding is desired for the reader, the first procedure can be used, with the encoding being
specified for the InputStreamReader:
```
   Charset utf8 = Charset.forName("UTF-8");
   FileInputStream inputFile = new FileInputStream("info.txt");
   InputStreamReader reader = new InputStreamReader(inputFile, utf8);
```
 - This reader will use the UTF-8 character encoding to read the characters from the file. Alternatively, we can use one
of the FileReader constructors that accept a character encoding.
```
   Charset utf8 = new Charset.forName("UTF-8");
   FileReader reader = new FileReader("info.txt", utf8);
```
 - A BufferedReader can also be used to improve the efficiency of reading characters from the underlying stream.

##### Using Buffered Writers
 - A BufferedWriter can be chained to the underlying writer using one of the below :
```
   BufferedWriter(Writer out)
   BufferedWriter(Writer out, int size)
```
 - In addition to the methods provided by the __Writer__, the BufferedWriter class provides the method newLine() for
writing the platform-dependent line separator.
 - The following methods creates PrintWriter whose output is Buffered.
```
   1. Charset utf8 = Charset.forName("UTF-8");
      FileOutputStream outputFile = new FileOutputStream("info.txt");
      OutputStreamWriter outputStream = new OutputStreamWriter(outputFile, utf8);
      BufferedWriter bufferedWriter = new BufferedWriter(outputStream);
      PrintWriter printWriter = new PrintWriter(bufferedWriter, true);
      
   2. FileWriter fileWriter = new FileWriter("info.txt");
      BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);
      PrintWriter printWriter = new PrintWriter(bufferedWriter, true);
```

##### Using Buffered Readers
 - A BufferedReader can be chained to the underlying reader by using one of the following constructors:
```
   BufferedReader(Reader in)
   BufferedReader(Reader in, int size)
```
 - In addition to the methods provided by the Reader class, the BufferedReader class also provides the method readLine()
, to read a line of text from the underlying reader.
 - The BufferedReader class also provides the lines() method to create a stream of text lines with a buffered reader as 
the data source.
```
   Stream<String> lines()
``` 
 - The following methods are used to create a BufferedReader to read a line of text :
```
   1. // Using the UTF-8 character encoding:
      Charset utf8 = Charset.forName("UTF-8");
      FileReader     fileReader      = new FileReader("lines.txt", utf8);
      BufferedReader bufferedReader1 = new BufferedReader(reader)

   2. // Use the default encoding:
      FileReader     fileReader      = new FileReader("lines.txt");
      BufferedReader bufferedReader2 = new BufferedReader(fileReader);
```

##### The Standard Input, Output and Error streams
 - The Standard output stream(usually the display) is represented by PrintStream object System.out
 - The Standard input stream(usually the keyboard) is represented by the InputStream object System.in
 - The Standard error stream(usually the display) is represented by System.err, which is another object of the PrintStream
class.
 - The __PrintStream__ class offers print() methods that act as corresponding print() methods from the __PrintWriter__ class.
 - In other words, both System.out and System.err act like PrintWriter, but in addition they have write() methods for writing bytes.
 - The System class provides the methods setIn(InputStream), setOut(PrintStream), and setErr(PrintStream) that can be 
passed an I/O stream to reassign the standard streams.
 - 