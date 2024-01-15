# Program Output

 - Data Produced by a program is called output, and it can be directed to different devices as required.
 - A Java program can send its output to terminal window using an object called Standard Output.
 - This Standard Output Object is found in class System as a static final object, and the object is of class
java.io.PrintStream(System.out).
 -  This class provides methods for printing values. These methods convert values to their text representation 
and print the resulting string.
 - The toString method of an object is called implicitly, if not explicitly before printing the object.
 - println() terminate the current line and print() doesn't.

----------------------------------------------
## Formatting
 - Not in any Java Developer Exam.
 - PrintStream printf(String format, Object... args)
// returns the object on which the method is invoked.
 - Any error in the format string will result in a runtime exception.

#### Format Specifier
 - %{-}nd > n specifies the number of characters and is always right justified. '-' can alter justification.
 - %{-}n.mf > n is the total number of chars and m is the number of chars in the decimal places.
e.g. %.2f, %6.4f. By default, decimal part takes 6 places. If less is allocated than what is there, then will be rounded 
off.
 - similarly for string, %{-}ns.