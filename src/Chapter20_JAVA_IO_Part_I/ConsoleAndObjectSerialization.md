## Console Class And Object Serialization
 - A console is a unique character based device associated with a JVM.
 - Whether a JVM has a console depends on the platform and the manner in which it is invoked.
 - If JVM is started from the command line, and standard I/O is not redirected, the console corresponds to keyboard and
display.
 - It is represented by the class java.io.console and is a singleton class and is obtained by System.console(). If there
is no console associated then null is returned.

#### The following functions are provided by console class :
 - Prompt and read a line of character-based response
```
    String username = console.readLine("Enter the username (%d chars): ", 4);
```
 - Prompt and read passwords without echoing the characters on the console.
```
    char[] password;
    do {
        password = console.readPassword("Enter password (min. %d chars): ", 6);
    } while (password.length < 6);
```
 - Like PrintWriter and PrintStream classes, the console class also provides format() and printf() methods but don't
allow locale to be specified.
 - The console class only returns character-based input. For reading other types of values from standard input stream,
the java.util.Scanner class can be considered.

```
// The first method reads a single line of text. The second method also prompt the message in addition.
    String readLine()
    String readLine(String format, Object... args)
    
// Echoing is disabled, and both reads a password or a password phrase. The second method also prints a prompt
    char[] readPassword()
    char[] readPassword(String format, Object... args)

// This retrieves the unique Reader object associated with this console.
    Reader reader()

// This retrieves the unique PrintWriter object associated with this console.
    PrintWriter writer()

// Flushes the console and forces any buffered output to be written immediately
    void flush()
```

## Object Serialization
 - Object serialization allows the state of an object to be transformed into a sequence of bytes that can be converted 
back into a copy of the object(called deserialization).
 - After deserialization, the object has the same state as it had when it was serialized, barring any data members that 
were not serializable. 
 - This mechanism is generally known as persistence—the serialized result of an object can be stored in a repository from
which it can be later retrieved.
 - Java provides the object serialization facility through the ObjectInput and Object-Output interfaces, which allow the
writing and reading of objects to and from I/O streams.
 - These two interfaces extend the DataInput and DataOutput interfaces, respectively.
 - The ObjectOutputStream class and the ObjectInputStream class implement the Object-Output interface and the ObjectInput
interface, respectively, providing methods to write and read binary representation of both objects and Java 
primitive values.
![ObjectStreamChaining](/Resources/ObjectStreamChaining.jpg)
 - The read and write methods in the two classes can throw an IOException, and the read methods will throw an EOFException
if an attempt is made to read past the end of the stream.

#### ObjectOutputStream Class
 - The class ObjectOutputStream can write objects to any stream that is a subclass of the OutputStream—for example, to a
file or a network connection (socket).
```
    ObjectOutputStream(OutputStream out) throws IOException

    FileOutputStream outputFile = new FileOutputStream("obj-storage.dat");
    ObjectOutputStream outputStream = new ObjectOutputStream(outputFile);

//  Objects can be written to the stream using the writeObject() method of the Object-OutputStream class:

    final void writeObject(Object obj) throws IOException
```
 - java.io.Serializable is a marker interface and only objects implementing this are serializable and thus can be passed
writeObject() method of ObjectOutputStream.
 - The String class, the primitive wrapper classes, and all array types implement the Serializable interface.
 - A serializable object can be any compound object containing references to other objects, and all constituent objects
that are serializable are serialized recursively when the compound object is written out. 
 - This is true even if there are cyclic references between the objects. Each object is written out only once during serialization.
 - The following information is included when an object is serialized:
   1. The class information needed to reconstruct the object
   2. The values of all serializable non-transient and non-static members, including those that are inherited
 - A checked exception of the type java.io.NotSerializableException is thrown if a non-serializable object is encountered
during the serialization process.
 - Note also that objects of subclasses that extend a serializable class are always serializable.

#### ObjectInputStream
 - An ObjectInputStream is used to restore (deserialize) objects that have previously been serialized using an ObjectOutputStream.
```
   ObjectInputStream(InputStream in) throws IOException

   FileInputStream inputFile = new FileInputStream("obj-storage.dat");
   ObjectInputStream inputStream = new ObjectInputStream(inputFile);
```
 - The readObject() method of the ObjectInputStream class is used to read the serialized state of an object from the stream:
```
   final Object readObject() throws ClassNotFoundException
```
 - Objects and values must be read in the same order as when they were serialized.
 - Serializable, non-transient data members of an object, including those data members that are inherited, are restored 
to the values they had at the time of serialization.
 - For compound objects containing references to other objects, the constituent objects are read to re-create the whole 
object structure.
 - In order to deserialize objects, the appropriate classes must be available at runtime.
 - Note that new objects are created during deserialization, so that no existing objects are overwritten.
 - Duplication is automatically avoided when the same element is serialized several times. E.g. If we've an array of string
objects, which is written and also the string object(s) in that array are written explicitly. Then the serialization 
happens only once.

##### Selective Serialization
 - static fields(not a part of objects) and fields declared with the modifiers transient(used for sensitive information) 
are not serializable.
 - Selective serialization discussed here is not applicable to record classes.
 - A compound object with its constituent objects is often referred to as an object graph. Serializing a compound object
serializes its complete object graph—that is, the compound object and its constituent objects are recursively serialized.
 - If the constituent objects of a compound object are not serializable (.i.e. doesn't implements Serializable), then an
exception of java.io.NotSerializableException.

##### Customizable Object Serialization
 - It isn't possible that all the classes that we make as a constituent of a compound object are Serializable. They may
also be final classes prohibiting any further extension. The client may not have access to the code. In these cases,
customizable Serialization is used for serializing such constituents.
 - Customized serialization discussed here is not applicable to record classes.
 - Any serializable object has the option of customizing its own serialization if it implements the following pair of methods:
```
     private void writeObject(ObjectOutputStream) throws IOException;
     private void readObject(ObjectInputStream)
                       throws IOException, ClassNotFoundException;
```
 - These methods are not part of any interface. Although private, these methods can be called by the JVM.
 - The first method above is called on the object when its serialization starts. The serialization procedure uses the 
reference value of the object to be serialized that is passed in the call to the __ObjectOutputStream.writeObject()__ method,
which in turn calls the first method above on this object.
 - The second method above is called on the object created when the deserialization procedure is initiated by the call to
the __ObjectInputStream.readObject()__ method.
 - In order to implement custom deserialization, we write the following lines of code in the writeObject method discussed
above. The first method does the normal serialization of the current object. The second method writes the field value of the __not serializable__
object, which is also declared transient in order to avoid java.io.NotSerializableException exception. The second line of
code is doing the customization of serialization and the same order will be followed in the deserialization process.
```
   oos.defaultWriteObject();               // Method in the ObjectOutputStream class
   oos.writeInt(wheel.getWheelSize());     // Method in the ObjectOutputStream class
```
 - For custom deserialization, the InputStream is read in the same order as it was written out inside the readObject 
method discussed above.
```
   ois.defaultReadObject();                // Method in the ObjectInputStream class
   int wheelSize = ois.readInt();          // Method in the ObjectInputStream class
   this.wheel = new Wheel(wheelSize);
```
 - Again, code for customization can be called both before and after the call to the defaultReadObject() method, as long
as it is in correspondence with the customization code in the writeObject() method.

##### Serialization and Inheritance
 - If the all the superclasses are serializable for a class then the state of the object during deserialization is same 
as during serialization.
 - This is because the normal Object creation and initialization procedure using constructors is __not__ run during 
deserialization.
 - If a superclass is not serializable then the object is created using no-arg constructor or default constructor for all
the non-Serializable class. And since the super constructors may have initialized the state of teh object, the object state
at deserialization differs.
 - If the non-serializable superclass does not provide a non-argument constructor or the default constructor, a 
java.io.InvalidClassException is thrown during deserialization.

###### Superclass is serializable
 - If the superclass is serializable, then any object of a subclass(even if it does not implement serializable interface)
is also serializable.

###### Superclass is Not Serializable
 - If the superclass is not serializable, then the super constructors are called during deserialization that could set some
fields to null, and hence before-after state of serialization-deserialization will not match.
 - If the default constructor is not provided, then java.io.InvalidClassException exception is thrown.
 - So the crux is, the superclass should be serializable or should provide no-arg constructor to avoid the exception.

##### Serialization and Versioning
 - The class versioning is required when a class is serialized using one class definition and deserialized using another
class definition.
 - If we use different class definition for serializing and deserializing respectively.InvalidClassException is thrown at
runtime.
 - serialVersionUID is a field in a serializable class, which is automatically assigned a value based on the definition
or can be assigned explicitly by the user as below :
```
   static final long serialVersionUID = 100L;            // Appropriate value.
```
 - SerialVersionUID is also stored in the serialized object(though static members aren't serialized, this one is an exception)
, which is compared with the deserializing class serialVersionUID
 - If not provided serialVersionUID is implicitly generated. If we define it ourselves, we can control what happens at 
deserialization. Maybe we can keep the serialVersionUID same for two different definitions of classes for deserialization
if it is not deemed that older streamed objects are no longer compatible for deserialization.
 - For e.g., if we've two Item classes with same serialVersionUID, one having only price field and other also having 
weight field. If we serialize an object with the first class and deserialize it with later one, the deserialization will 
be successful with weight field initialized with 0 value and the other matching fields having the same value.
 - But different SerialVersionUID will cause deserialization error. It is the best practice to use SerialVersionUID with
serializable classes.

