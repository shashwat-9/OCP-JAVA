# Conversions

###### Widening and narrowing Primitive Conversions
For Primitive data type, the value of a narrower data type can be converted to a value of wider data type. This is 
called widening primitive conversion.

![TypeConversion](./Resources/TypeConversions.jpg)

Conversions are transitive, meaning int can be directly converted to double, without going through the arrow.

Converting from a wider primitive type to a narrower primitive type is called a narrowing primitive conversion.
 - Conversion from char to two integer types byte, short is considered narrowing primitive conversions due to possible
lossy conversion.
 - Widening primitive conversions are done implicitly, whereas narrowing primitive conversion usually require a cast.
 - It's not illegal to use a cast for widening conversion.
 - Regardless of any loss of magnitude or precision, widening and narrowing primitive conversions never result in 
runtime exceptions.

###### Widening and Narrowing Reference Conversions
The subtype-superType relationship between reference types determines which conversions are permissible between them.
 - Conversion up the type hierarchy is called widening reference conversion(upcasting).
```
    Object obj = "Upcast me";   // Widening: Object is supertype
```
 - Conversions down the type hierarchy represent narrowing reference conversions(downcasting).
```
    String str = (String) obj;  // Narrowing: Object is supertype
```