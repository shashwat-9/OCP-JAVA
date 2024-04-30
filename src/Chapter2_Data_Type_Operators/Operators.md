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

#### Arithmetic Operators
 - Operands are of numeric type(that includes char).
 - Now floating point operations are strict, meaning they will give the same result on any jvm implementation.
 - Earlier _strictfp_ used to enforce this behaviour.

##### Arithmetic Operators precedence and associativity

- The rows in the table below are in descending order of precedence.
- The operators in the same row have the same precedence.
- The unary operators have right associativity, and the binary operators have left associativity.

| Type   | Operator1 | Operator2 | Operator3 |
|--------|-----------|-----------|-----------|
| Unary  | +         | -         |           |
| binary | *         | /         | %         |
|        | +         | -         |           | 

##### Evaluation order in arithmetic expression
 - Java guarantees that the operands are fully evaluated from left to right before an arithmetic binary operator is 
applied.
 - If an operand evaluation results in error, then subsequent operands are not evaluated.
 - (a + b * c), here a is evaluated first, b second, c in the last, but the binary operator is applied as per the 
precedence.

##### Range of Numeric Values
 - The range of numeric types are given by _MAX_VALUE_ and _MIN_VALUE_ in their respective Wrapper Class(es).
 - Arithmetic operators are overloaded, that is, when any of the operand is floating point, then the evaluation is
floating point type, else it is integer arithmetic.

##### Integer Arithmetic
 - ArithmeticException occurs when division or remainder is by zero(0).
 - Integer arithmetic always returns a value that is in range, except the above case( and including cycle-addition).

##### Floating point Arithmetic
 - Adding or multiplying two very large floating point numbers result in an out-of-range value that is represented by 
infinity.(This behaviour is different to that of integer arithmetic)
 - Division by zero also returns infinity.
 - Infinity could be + or -, represented by constants POSITIVE_INFINITY and NEGATIVE_INFINITY respectively in both Float
and Double class.

![FloatPoint](./Resources/FLoatingPoint.jpg)
 - Underflow occurs when the result is between Double.MIN_VALUE and zero. It returns positive zero.
 - Or the result is between -Double.MIN_VALUE and zero. Underflow then returns negative zero(-0.0).
 - (-0.0 == 0.0), is true, that is negative and positive zeros are equal.

 - Certain calculations have no results and are represented by NaN(Not a Number). Example include, division of zero by 
zero, finding square root of -1 and other invalid calculations.
 - NaN is represented by a constant in java.lang.Float or java.lang.Double
 - Any operation involving NaN will produce NaN.
 - Any comparison(except !=) involving NaN return false. Inequality (!=) comparison involving NaN always return true.
 - A recommended way of checking whether a value is NaN or not, is to use the method isNaN(), in java.lang.Float or 
java.lang.Double.
 - Note, these are for floating point and not integer arithmetic.

##### Unary Arithmetic Operators : -, +
 - Unary (-) operator negates the numeric value of its operand. e.g. - -10, this results in 10. Space is required in between 
to avoid using the decrement operator(--) on constant literal.
 - Unary (+) has no effect on the evaluation on operand value.

##### Multiplicative Binary Operators : * / %
###### Multiplicative Operator : *
 - It multiplies two numbers.
###### Division Operator : /
 - Division Operator is overloaded. The result is of type integral if both are integers and of floating point type if 
atleast one is of floating point type.
 - 