## Operators

### The Assignment Operator
Syntax for assignment is :
```
target = expression
```
 - target is a variable declared before, and expression must be assignable to the target variable.
 - previous value is overridden, and the type of target variable must be either primitive or reference.

#### Assigning primitive value
The assignment operator has the lowest precedence and thus the expression on the right is evaluated first.

#### Assigning references
Assigning a reference variable to another reference variable simply makes the variable point to the new reference and
doesn't create a copy or assigns the state of the object to the object of the target variable.

#### Multiple Assignments
Assignment is an expression and the value of the target variable is returned by the expression.
```
int j, k;
j = k = 10;
// k is assigned the value of 10, which is being returned and is assigned to j
```
 - Multiple assignment(s) holds true similarly for reference variable.
 - The below example will not compile as v2 is not declared.
```
int v1 = v2 = 2016;            // Only v1 is declared. Compile-time error!
```

#### Type Conversion in assignment context
If the source value is NOT of the same type of the target variable, then if widening conversion is permissible, it is 
done implicitly.

 - A widening primitive conversion could lead to a loss in precision. For e.g.
```
long bigInteger = 98765432112345678L;
float fpNum = bigInteger;  // Widening but loss of precision: 9.8765436E16
```

Additionally, implicit narrowing primitive conversions on assignment can occur in cases where all of the following 
conditions are fulfilled:
 - The source is a constant expression of type byte, short, char, or int.
 - The target type is of type byte, short, or char.
 - The value of the source is determined to be in the range of the target type at compile time.

A constant expression is an expression that either denotes a primitive value or a string literal. Composed of operands
that are only _literals_ or _constant variable_ and the operators that are evaluated on compile time only(arithmetic, 
comparison operator and not runtime function calls, increment/decrement etc).

 - A _constant variable_ is a final variable of either primitive or String type that is initialized with a constant 
expression.
 - If the above 3 conditions aren't satisfied for narrowing primitive conversion on assignment, then compile time error
will occur, else we will have to cast the value to the target or apt type.

```
int i2 = -20;            // i2 is not a constant variable. i2 is not final.
final int i3 = i2;       // i3 is not a constant variable, since i2 is not.
final int i4 = 200;      // i4 is a constant variable.
final int i5;            // i5 is not a constant variable.

All of the below will give compile time error, as value range can't be evaluated on compile time.

short s3 =  i2;   // Not constant expression.
char  c3 =   i3;   // Final value of i3 not determinable at compile time.
char  c4 =   i2;   // Not constant expression.
byte  b4 =   128;  // int value not in range.
byte  b5 =   i4;   // Value of constant variable i4 is not in range.
i5 = 100;                // Initialized at runtime.
short s4 =  i5;   // Final value of i5 not determinable at compile time.
```
 - Floating point values are truncated when cast to integral values.
 - The discussion of numeric assignment conversions also applies to numeric parameter values at method invocation , 
except for the narrowing conversions, which always require a cast.
 - Same goes for boxing/un-boxing assignments.
