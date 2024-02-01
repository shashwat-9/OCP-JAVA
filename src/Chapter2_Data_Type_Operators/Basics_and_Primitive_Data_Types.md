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
