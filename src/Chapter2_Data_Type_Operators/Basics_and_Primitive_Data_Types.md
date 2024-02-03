# Basic Language Elements
The basic language elements include low level elements using which high level constructs are formed.

### Lexical Tokens
Low level elements like Identifiers, numbers, operators, special character are called lexical token used to build 
high level constructs like expressions, statements, methods, and classes.

#### Identifier
Any name in the program is called an identifier, used to denote the name of classes, methods, variables and labels.
 - The identifier is named as a sequence of characters and digits, with the rule that identifier doesn't start with 
a digit.
 - The java program uses Unicode character set and thus the allowed character could be from different languages.
 - Underscore '_'(with other characters) and _currency_ symbols(such as $, ¢, ¥, or £) are also allowed.
 - '_' on itself is not a legal identifier but is a keyword in java(in SE17).

#### Keywords
Keywords are reserved words in java that can't be used as identifiers, that can't be used for naming any other entity.
 - All java keywords are lowercase and incorrect usage leads to compile-time error.
 - There are 3 types of keywords :
   1. Reserved Keywords. e.g. continue, while, synchronized, for, while etc
   2. Contextual keywords - restricted in certain context. e.g. exports, uses, opens, sealed.
   3. Reserved but not in use. e.g. goto, const

 - In addition, three identifiers are reserved, namely - true, false, null.

#### Separators
Separators(also known as _punctuators_) are tokens aiding compiler in syntax and semantic analysis.
 - {},(),[], ., ;, ..., @, ::
 - {} is used to contain a set of statements. Like-wise all separators have functions.

#### Literals
Literals are constant values in a java program. The values could be of all data types - int, char, float, boolean,
String.

##### Integer Literal
Integer data type comprises the following primitive data types - int, long, byte, short.

The default type for integer literal is int. For long, the literal should be appended with 'l' or 'L'. There is no
specification for short or byte.

Integer literal can be represented into all the number systems - namely binary, octal, decimal, hexadecimal.
 - binary - prefixed with '0b' or '0B'
 - octal - prefixed with '0'
 - hexadecimal - prefixed with '0x' or '0X'

Suffix 'l' or 'L' of long type and - sign can be added regardless of the number system used.

###### Representing Integers
 - Integer data types can represent both positive and negative values.
 - Value of Char types can be regarded as 16-bit unsigned integer.
 - Java uses two's complement to store signed values of integer.
 - In bit representation, the MSB(Most Significant Bit) represents the sign of the integer.

###### Calculating two's complement
 - A number's 2-s complement is used to represent a negative number.
 - One's complement of a number is calculated by inverting all its bits in binary form. Represented by ~N.
 - Two's complement of a number is : 

```
   -N = ~N + 1; // One plus one complement of the number is negative of that number
```

 - Even subtraction is considered as a sum of a number with another number's 2-s complement.
 - As another matter of fact, byte, short, int, long are of size 8, 16, 32 and 64 bits.

##### Floating points Literals
This has two types, 1. Float 2. Double
 - Default type for this literal is double, that can be explicitly designated by appending 'D' or 'd'.
 - This literal can be assigned the type of float by appending with 'f' or 'F'.
 - Floating point literal can also be represented in scientific notation with exponent('E' or 'e'). 
```For e.g. - 1.95e3  = 1.95 * 10^3 = 1950```

 - E.g. of floating point literal.  
49., 49.0D, 49.0, 49D, 4.9e1, 4900e-2 etc represents double.  
49.f, 4.9e1f, 49F etc represents float. 

The decimal point(49.f/d can be represented as 49f/d) and exponent are optional.

##### UnderScores in Numeric Literals
