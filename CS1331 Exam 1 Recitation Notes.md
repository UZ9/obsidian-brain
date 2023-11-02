[[CS1331 MOC]]
# Recitation 1
- javac = compile a .java class -> .class file(s)
- java = run already compiled .class files

Example: TestClass.java
`javac TestClass.java` - outputs TestClass.class
`java TestClass` - runs TestClass.class

# Recitation 2
#### Differences between declaring, assigning, and initializing

**Declaring** - declares type (e.g. int, String) but does NOT assign it a value

```java
int myInt; // Declares a variable with name 'myInt' and type 'int'
```

**Assigning** - assigning a value to the variable (NOTE: declare & assign can be on same line)

```java
// Assuming myInt was already declared somewhere else
myInt = 3; // Assigns the value 3 to myInt
```

**Initializing** - assigning a value to a variable for the *first time*

```java
int myInt = 3; // Assigns value of 3 for the first time

myInt = 4; // This is NOT initialization -- it's not the first time
```

#### Variable Naming Requirements
- can't be reserved word (`int`, `public`, `class`, `static`, etc)
- cannot **start with a number**
- cannot contain special characters **EXCEPT** $ and _ (but these are discouraged)

#### Variable Naming Conventions
- Camel case (`thisIsTheNameOfAVariable`) (note that you'll see this being called upperCamelCase most of the time, but the recitations call it just camel case)
- Descriptive name (`speed = distance / time` rather than `c = a / b`)

![[Pasted image 20230921002532.png]]

### Variable Types

#### Primitives
- hold the value itself (**NOT** a reference!)
- primitive types are always lowercase
- **8 types**: 
	- Integer: byte, short, int, long (in order of size)
	- Floating: float, double (in order of size/precision)
	- Other: char, boolean

#### Reference Types
- Hold a **reference** to a value (ALL OBJECTS ARE REFERENCE TYPES)
- This is discussed much more in *Recitation 04*

### Literals

- Any constant assigned to a variable
	- `12.0`, `31`, `"Andrew"`
- **ALL** number, char, boolean, String, and enum values are literals

![[Pasted image 20230921003005.png]]

### Immutability
**final** - variable is marked is *immutable*, in which it cannot be changed (official wording of recitation)

> [!Info]
> For constants, naming convention is UPPERCASE_AND_UNSCORES
> 
> Example:
> ```java
> final double EARTH_GRAVITY = 9.81;
 >``` 


### Operator Cheat Sheet
![[Pasted image 20230921003235.png]]

### IMPORTANT - ++i vs i++
**i++** - increment i, but return the *original value*

**++i** - increment i, return *incremented value* 

```java
int a = 2;
int b = a++; // b = 2, a = 3

int c = 2;
int d = ++c; // d = 3, c = 3
```

### Type Conversion (Important)
**Widening** - small to big conversion, e.g. byte -> int

**Narrowing** - big to small, e.g. double -> int
- REQUIRES EXPLICIT CAST, or else there is an error


### Types of Casting
**Explicit Casting** - Used when there could be a *loss* of data, e.g. narrowing 

```java
(byte) 12 // Uses parentheses to designate casting
```

**Implicit Casting** - Automatic casting done by Java
```java
double e = 3; // 3 is being implicitly cast to double, widening 
```

> [!INFO] 
> Widening, e.g. 3 to 3.0, is often considered a **promotion**. 

#### Comments

**Single Line**
```java
// This is a single-line comment
```

**Multi-line (Block)** (astericks in middle are OPTIONAL)
```java
/*
* This is 
* a block
* comment
*/
```

#### Topic Trivia

![[Pasted image 20230921003819.png]]


# Recitation 3
#### Short-Circuit Evaluation (VERY IMPORTANT, EXAM QUESTION)
- If logical expression can be determined before the end of testing all parts of it 

OR example:
```java
// Java sees 3 + 4 is indeed true, so there's no point in checking the rest as || requires only one to be true, preventing a divide by zero error
if (3 + 4 == 7 || 4 / 0 == 3) {

}
```

AND example:
```java
// Java sees that 3 + 4 isn't 994, so there's no point in checking the rest as && requires both to be true, preventing a divide by zero error
if (3 + 4 == 994 && 4 / 0 == 3) {

}

```

#### Note on if-else conditions
- *Trick Question* - If statements without brackets **only run the first line**

Example:
```java
if (userIsLoggedIn)
     System.out.println("User is logged in successfully.");
     showBankInformation(); // This is NOT in the if statement, resulting in the bank information being shown REGARDLESS of whether the user is actually logged in or not 
```
is equivalent to:

```java
if (userIsLoggedIn) {
	System.out.println("User is logged in successfully.");
}
showBankInformation();
```

*Trick Question* - Else statements are connected to the inner-most if statement 

```java
if (condition)
if (condition2)
	System.out.println("Yippee");
else 
	System.out.println("Whoops");
```

is equivalent to:

```java
if (condition) {
	if (condition2) {
		System.out.println("Yippee");
	} else {
		System.out.println("Whoops");
	}
}```


#### Ternary Operators
Format: `<some condition> ? <value if true> : <value if false>`

Example conversion:
```java
if (2 * 4 == 8) {
	mySanity = "Good";
} else {
	mySanity = "Concerning";
}
```

is equivalent to:
```java
mySanity = 2 * 4 == 8 ? "Good" : "Concerning";
```

### Switch Statements
- Used for conditionals with many different cases
- Works with byte, short, int, char, String, enum
- break - USED FOR AVOIDING FALL THROUGH

```java
char letterGrade = 'A';

switch (letterGrade) {
// Note: same indention level as the switch itself, it's NOT indented
case 'A': 
	System.out.println("90-100");
	break;
case 'B':
	System.out.println("80-89.99");
	break;
case 'C':
	System.out.println("70-79.99");
	break;
case 'D':
	System.out.println("60-69.99")
	break;
default:
	// if letterGrade is not any of the above, run default
	System.out.println("Yeet");
}
```
Important Notes:
- If you **don't have the break** (*Trick Question*), the code will continue onto the next case (A might print all of the other statements as well, including the default)

- You can intentionally not add breaks if you want multiple cases doing the same thing, e.g.
```java
switch (letterGrade) {
case 'A':
case 'B':
case 'C':
	System.out.println("You passed!"); // prints if letter is A, B, or C
	break;
default: 
	System.out.println("uh oh");
}
```

### Loops
#### For Loops
- 3 components: `initializer`, `condition`, `update`

```java
for (initializer; condition; update) {
	// loop body
}
```

*Trick Question*: If you accidentally add a semi colon after the parentheses, the loop will run exactly **once**:

```java 
for (initializer; condiiton; update); {
	// this only runs once
}
```

This is due to it becoming the equivalent of this:

```java
for (initializer; condition; update);

// whatever code was in the brackets
```

**For Loop Workflow**
- Initializer is executed exactly **once**
- Condition is checked **before** each iteration (INCLUDING BEFORE FIRST)
- Update is executed **after** each iteration (after loop body)

Use for loops when you know *exactly* how many times to loop

#### While Loops
- Executes *while* the conditional statement is true 
- Conditional evaluated **before** the loop body 
- If it never becomes false, the loop will be **infinite**
- Use it when you don't know how many times it repeats

```java
while (condition) {
	// loop body
}
```

#### Do-While Loops
- **VERY IMPORTANT DIFFERENCE** - conditional is evaluated **AFTER** the loop body
- The loop is guaranteed to run *at least once*

```java
do {
	// loop body
} while (condition);
```

### break and continue keywords
**break** - terminates *inner most loop* (in other words, outside of the brackets)

```java
for (int i = 0; i < 16; i++) {
	if (i % 2 == 0) {
		continue; // Continue skips to the end
	}
	
	if (i >= 10) {
		break; // This would end the for loop
	}
}

// After the break, the code continues here
```

### Topic Trivia

![[Pasted image 20230921010125.png]]

# Recitation 04

#### Reference Types (Objects and Classes)
- Variables that **store a reference to an object's location in memory**
- Reference types start with uppercase

```java
String str1 = "Hello!"; // Special method of initializing reference type (string pool)
String str2 = new String("Hello!"); // Normal way of initializing reference types for all other objects
```

### Strings 
**IMPORTANT** - STRINGS ARE IMMUTABLE - THEY CANNOT BE MODIFIED

String concatenation:
```java
"H" + "E" == "HE"
```

#### String Methods
**All string methods return a NEW STRING**

*Trick Question*
```java
String e = "Hello!";

e.toUpperCase(); // THIS DOES NOTHING TO THE CONTENTS OF E
```

Example methods:
- concat (adds two strings, not commonly used)
- indexOf (gets the index of a string/character within a string)
- length() *Trick Question* - length is a **method** and requires the parentheses
- replace(char old, char new) - replaces **all** instances of a character with another
- substring(int beginIndex, int endIndex) - retrieves characters from (beginIndex, inclusive) to (endIndex, exclusive) *Trick Question* - END INDEX IS EXCLUSIVE!!!!
- toUpperCase()
- toLowerCase()
- compareTo(String)
#### indexOf Method
```java
String test = "Hello there this is cool!"

System.out.println(test.indexOf("this")); // prints 12
```
#### compareTo Method
- Compares strings **lexicographically** (alphabetical), and is **case sensitive**

![[Pasted image 20230921011224.png]]

Think of it as this way:

a.compareTo(b) does the following:
- Loops through and finds the value for every character for `a`, and adds them all up
- Loops through and finds the value for every character for `b`, and adds them all up
- Returns the sum value of `a` minus the sum value of `b`
- To check if something is above or below you would use `> 0` or `< 0`

#### equals()
- Strings should **ONLY BE COMPARED** with equals()
- Compares the **values**, NOT the references

```java
String s1 = "ABC";
String s2 = new String("ABC");

System.out.println(s1 == s2) // false, difference reference types
System.out.println(s1.equals(s2)) // true, values are the same
```

#### Object Aliasing
- Object can be accessed through multiple alias names 
- **Consequence** - if object is mutable, modifying alias *will* modify original

```java
String s1 = "hello";
String s2 = s1; // this is an alias of the s1 reference

System.out.println(s1 == s2); // true
```

#### Topic Trivia

![[Pasted image 20230921011726.png]]

#### Command Line Output
`System.out.print()` - Prints on the **current line**

`System.out.println()` - Prints on the current line, and then **adds a new character (`\n`) line to the end**
- Equivalent to `System.out.print(message + "\n")

`System.out.printf()` - Prints with formatters (see below)

#### printf() syntax
- Syntax of printf:
`%[flags][width][.precision]conversion-character`

`flags` - (optional) modifies output format

`width` - (optional) sets minimum # of characters

`precision` - amount of decimal places OR characters (depending on data type)

`conversion character` - type of conversion

#### Conversion Character List

`s` - String
`d` - Decimal integer (use it for int)
`f` - floating-point (use it for floats, doubles)
`b`, '`B`' - false/FALSE or true/TRUE *probably won't show up*
`c` - unicode character *probably won't show up*

Example:

`System.out.printf("%9.3f", 3.14)
- 9 **minimum characters** total (*Trick Question*: **INCLUDES THE DECIMAL PLACE in size**)
- **ROUND** to 3 decimal places

3.14 becomes 3.140

3.140 is 5 characters, therefore **4 spaces are added to beginning**

#### Console I/O: Scanner
**Uses the import: ** `java.util.Scanner`

Format for declaring: (DON'T FORGET THE `System.in`)
`Scanner scanner = new Scanner(System.in);`

- Don't declare more than one scanner for System.in!!!

![[Pasted image 20230921012419.png]]

*Scanner Gotcha*

```java
int i = scanner.nextInt(); // LEAVES THE NEW LINE AFTERWARDS

scanner.nextLine(); // YOU HAVE TO CLEAR REST OF LINE

String s = scanner.nextLine(); // Now this works
```

#### Package Improts

```java
import packagename;
```

Example:
```java
import java.util.Scanner;

// Not recommended: import EVERYTHING from java.util
import java.util.*;
```

#### java.lang.Math class
- ALREADY IMPORTED - NO NEED FOR INPUT

Contains useful math expressions:
- Math.sqrt
- Math.round
- Math.min
- Math.max
- Math.pow
- Math.abs
- Math.random() -- *Trick question* The range of Math.random() is `[0.0, 1.0)` IT DOES NOT INCLUDE 1.0
- All methods are static (don't declare Math)

#### java.util.Random 
- Allows pseudo-random number generation with customization
- REQUIRES YOU TO INITIALIZE A `Random` INSTANCE

```java
Random rand = new Random();

// BE VERY CAREFUL OF THE EXCLUSIVITY () vs [] OF THESE METHODS
rand.nextInt(); // int in range [-2147483647, 2147483647]
rand.nextInt(int bound); // returns int in range [0, bound)
rand.nextDouble(); // Returns double in range [0.0, 1.0)
```

### Enums
- Predefined unchangeable values (constants)

```java
public enum Season {
	SPRING, SUMMER, FALL, WINTER // notice these are commas, NOT semicolons 
}
```

**Important enum methods**
```java
// name() - name of enum element
Season.SUMMER.name() // returns "SUMMER"

// ordinal() - position of enum constant
Season.SUMMER.ordinal() // returns 1

// values() - returns all enum constants as an array
Season.values() // returns [SPRING, SUMMER, FALL, WINTER]
```

### Methods
**method definition** - consists of method header and method body

**method header** - consists of modifiers, return value type, method name, and parameters

**method signature** - method name and type of parameters (parameter list)

![[Pasted image 20230921013257.png]]

#### static Methods
- **DOES NOT** require a class to be instantiated to call these 

examples: `public static void main(String[] args) {...}`

`public static int myMethod(int someParameter) {...}`



#### Examples for method headers vs method signatures
```java
public static double sum(int a, double b) {
	return a + b;
}
```

Method header:
```java
public static double sum(int a, double b)
```

Method signature:
```java
sum(int, double)
```


#### Topic Trivia
![[Pasted image 20230921013528.png]]

# Recitation 05
#### Difference between argument and parameter
**Arguments** - values passed to method

**Parameter** - defines what values are put into a method 

```java
// a and b are parameters
public static int multiply(int a, int b) {
	return a * b;
}

public static void main(String[] args) {
	int product = multiply(3, 6); // 3 and 6 are arguments
}
```
#### Scope
- "how far in" the variable is in (NOTE: **INDENTIONATION DOES NOT MATTER**)

3 main types:
**Class level** - anywhere inside MyClass (`x` in example)

**Method level** - anywhere inside main (including the argument)

![[Pasted image 20230921092928.png]]

#### Scope Practice

![[Pasted image 20230921093429.png]]

#### Method Overloading

- More than one method with the **same name** but **different parameters**
	- they must have **different method signatures**

> [!Warning] 
> The *static* modifier of a method is **not** part of the method signature.

```java
// Method signature: int subtract(int, int)
public static int subtract(int a, int b) {
	return a - b;
}

// Method signature: double subtract(double, double)
public static double subtract(double a, double b) {
	return a - b;
}
```

#### Ambiguous Invocation
- Arguments passed into method don't match method signature of overloaded method
- Compiler will attempt to invoke (execute) method with **fewest conversions required**
- If two methods require the *same amount of conversions*, compiler **throws an error**

Example:
```java
public static void main(String[] args) {
	sum(1, 2); // Both possible methods require 1 conversion, ERROR
}

// Requires 1 conversion (promosion of second argument from int to double)
public static double sum(int a, double b) {
	return a + b;
}

// Requires 1 conversion (promotion of first arg from int to double)
public static double sum(double a, int b) {
	return a + b;
}
```
### Arrays
- *Objects* that represent a sequence (ordered) of homogenous (all the same type) elements
	- can either be primitive type or reference type
- Arrays are **mutable**
- Length is **fixed once instantiated**
- Arrays are **0 indexed** - attempting to grab `arr[arr.length]` *will throw an error*

![[Pasted image 20230921094520.png]]

#### Creating Arrays
**3 different ways to declare an array**
```java
int[] arr1 = new int[5]; // array is populated with zeroes (default int value)
int[] arr2 = new int[]{1, 2, 3, 4, 5}; // length is number of elements
int[] arr3 = {1, 2, 3, 4, 5}; // ONLY valid during declaration
```

> [!important] 
> Array length is **.length**, THERE ARE NO PARENTHESES

Accessing and setting elements:
```java
int[] arr = new int[8];

arr[3] = 4; // sets 4th value to 4

arr[3] // 4 

arr.length // 8
```


#### Enhanced For Loop
Easier way of looping through elements
NOTE: DO NOT USE THIS IF YOU NEED TO CHANGE ELEMENTS OF THE ARRAY

- Only iterates **forward**
- Doesn't use an `i` for knowing what index
```java
int[] arr = {1, 2, 3, 4};

for (int e : arr) {
	e *= 2;
	System.out.print(e + ",");
}

// prints 2,4,6,8,
// arr == {1,2,3,4}
```

#### Multi-Dimensional (Nested) Arrays
- Arrays are objects, and can **store other arrays**
- The length of the arrays *inside* of the array do **not** matter
```java
int[][] arr2D = new int[rows][cols]; // cols is optional

// jagged columns
int[][] jagged = new int[] {
	{1, 2, 3, 4},
	{5, 6, 7},
	{8, 9}
};
```

#### Array Aliasing : Array Shallow vs Deep Copy
**Shadow Copy** - copy of the reference (that still points to the same object)
- Problem with shadow: modifying an element of original array modifies copied array

**Deep copy** - entirely new object in memory - identical data to original object

```java
int[] nums = {1, 2, 3, 4}

// Copies the reference, both shallowCopy and nums still point to the same array
int[] shallowCopy = nums;

// Create an entirely new array in memory
int[] deepCopy = new int[nums.length];

for (int i = 0; i < nums.length; i++) {
	deepCopy[i] = nums[i]; // Manually add elements to new array
}

nums[2] = 0; // Modify nums

// Result of nums
nums // {1, 2, 0, 4}
shallowCopy // {1, 2, 0, 4}
deepCopy // {1, 2, 3, 4}
```

> [!Warning] Methods can **also** modify the original array!

Take this function:
```java
public static void processArray(int[] arr) {
	arr[2] = 99;
}
```

```java
int[] arr = { 1, 2, 3, 4 };

processArray(arr); // reference passed to process array

arr // { 1, 2, 99, 4 }
```

### IMPORTANT - Pass-by-value
- Java is **only** pass- by-value

- Every time a variable is passed into a method, a **copy** of that value is passed instead of a reference to that variable 
	- For primitive types (int, double, etc.) it is the **literal value**
	- For primitive-type variables it is the **reference (address)** to the object
		- This is seen in the above example with `processArray` - a copy of the reference is created

#### Check Style Guide (probably not on exam)
To run:
```sh
java -jar [path to checkstyle jar] [path to .java file]
```

Example:
```sh
java -jar checkstyle.jar TestClass.java
```