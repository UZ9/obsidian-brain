[[010 CS1331 MOC]]

# (Useful) things Landry has said on stream
### Clarification on Hashcode knowledge needed for exam
- You do **not** need to know how to write a hashcode method
- You **do** need to understand what a hashcode is (and why it's good practice to override it for equals())
- You do **not** need to compare hashcodes in .equals()

### Static Clarification
You **CANNOT** override static methods.

### Clarification on .equals
- If you are comparing **reference types** in .equals(), you **need to null check**.

Example:
```java
public class Person {
	// Note - override is not required, but recommended
	@Override
	public boolean equals(Object o) {
		// NOTE how this uses short circuit to prevent a null check
		if (o != null && o.getClass() == this.getClass()) {
			
		}
	}
}
```

Recitation 5
*Recitation 5 was right before Exam 1, and most of the time was dedicated to a review. As a result this section is shorter than usual recitations.*

### Scope
Think of the word **scope** and how we use it outside of CS: you might look through a lens of a microscope **to look at something small**, or attach a scope to a hunting rifle to **aim at a particular target** (idk i don't hunt, the specifics are unknown to me).

Much like these examples, **scope** is a "region" of code limiting what can be accessed from other areas. 

There are 3 primary types of scopes:

- **Class Level** - anywhere inside of a class

- **Method Level** - Anywhere inside of a method (in this example, the *main method*)

- **Block level** - Inside of a particular portion of code typically inside of a method, and surrounded by `{}`
![[Pasted image 20231016000132.png]]

*Fun fact:* You don't actually need some sort of statement to create a block level! The following is valid:

```java
public void someMethod() {
	int x = 3;

	{
		// The brackets created a block
	}
}
```

##### Scope Practice
![[Pasted image 20231016000832.png]]


### Method Overloading
Method overloading = **same name, different method signature**

```java
public static int subtract(int a, int b) {
	return a - b;
}

// VALID OVERLOAD
// Note that this method has the SAME name (subtract), but the parameters are DIFFERENT (double, double) 
public static double subtract(double a, double b) {
	return a - b;
}

// INVALID OVERLOAD
// This has the same signature (same name, same parameters) and will throw a compiler error (it's already defined).
public static double subtract(int a, int b) {
	return a - b; 
}

// INVALID OVERLOAD
// This has the same name, but different parameters. This will only create a new method, and is NOT considered an overload
public static double subtractIntegers(int a, int b) {
	return a - b;
}

```

#### (IMPORTANT) Ambiguous Invocation

> [!important] IMPORTANT
> Landry has mentioned several times about how "tricky" this concept is--and he LOVES tricky questions. 

If the arguments passed do **not** exactly match the method signature, the compiler will invoke (run) the method requiring the **least amount of parameter conversions**.

If there is **more than one** method requiring the same amount of conversions, the compiler **cannot determine** which will be invoked and throws an error.

```java
public static void main(String[] args) {
	sum(1, 2); // THIS WILL THROW A COMPILER ERROR
}

// Passing in (int, double) to a method (int, double)
// This requires the SECOND argument to be promoted to a double,
// requiring ONE total conversion
public static double sum(int a, double b) {
	return a + b;
}

// Passing in (int, int) to a method (double, int)
// This requires the FIRST argument to be promoted to a double,
// requiring ONE total conversion.
// Because the two methods requiring the fewest conversions are requiring the same amount, a compiler error will be thrown
public static double sum(double a, int b) {
	return a + b;
}
```

*Trick question* - This scenario will **ONLY** happen if those two methods happen to be the **LEAST** conversions required. If there was a third method requiring 0:
```java
// Passing in (int, int) to a method (int, int)
// This requires NO arguments to be changed,
// requiring ZERO total conversions.
// As a result, no compiler error will be thrown EVEN THOUGH TWO METHODS HAVE THE SAME AMOUNT OF CONVERSIONS.
public static double sum(int a, int b) {
	return a + b;
}
```

#### (IMPORTANT) Arrays

> [!warning] ARRAYS ARE OBJECTS, **NOT** PRIMITIVES! 
> This is extremely important when it comes to deep/shallow copies (Mentioned in detail later).
> 

Arrays = objects representing a **sequence** (order) of **homogenous** (same type) elements
- The types of elements CAN be primitives, e.g. int, or reference types
- **Capacity (length) is fixed and CANNOT be changed**.
- **Arrays start at 0, and end at length - 1**.

![[Pasted image 20231016002654.png]]

##### Creating Arrays
```java
// "type" is the type of whatever you're trying to store, e.g. "int" or "String"
type[] name = new type[length]

// ==========================
// Creating arrays (3 ways)
// ==========================

// Creates an array of the specified size (in this case 5) and fills it 
// with the DEFAULT value for that type.
// Note: populated = fill (means the same thing)
int[] arr1 = new int[5]; // Creates array of size 5 populated with 0

// Creates an array by directly passing values into it
// The length of the array will be the amount of elements, in this case 5
int[] arr2 = new int[] { 1, 2, 3, 4, 5 }; 

// Java is actually smart enough to know what type the array is, no new keyword needed!
int[] arr3 = { 1, 2, 3, 4, 5 };


// WARNING: EVEN THOUGH YOU CAN INITIALIZE IT WITHOUT THE NEW, YOU CANNOT SET IT THAT WAY AGAIN.
arr3 = { 1, 2, 3, 4, 5 }; // THROWS AN ERROR

// ==========================
// Retrieving array length
// ==========================

int arr = new int[3];

int len = arr.length; // Length is 3
int last = arr[2]; // REMEMBER THAT IT STARTS AT ZERO!!!
int first = arr[0];

arr[3] // THIS WILL THROW AN OUT OF BOUNDS EXCEPTION
```

#### for-each Loop (Enhanced for Loop)
- A much simpler way to loop through objects

**LIMITATIONS**
- No way of knowing what index you're currently at (unless you have another integer)
- **Cannot be used to modify the array**
- Can only iterate forward

```java
int[] arr = {1, 2, 3, 4};

for (int e : arr) {
	// e is the current value in the loop
	// this is as if we were doing int e = arr[i] in a traditional loop
	
	e *= 2;
	System.out.print(e + ",");
}

// prints 2,4,6,8,
// arr == {1,2,3,4}
```

#### Multi-Dimension (Nested) Arrays
- Arrays can store primitives or objects
- **Arrays are objects**

In other words, **arrays can store arrays**.

```java
// Where rows is an int, cols is an int
int[][] arr2D = new int[rows][cols];
```

*Trick Question*: Only the length of the outermost (rows in this case) array has to be specified. This is perfectly valid:
```java
int[][] arr2D = new int[rows][];

// Alternatively, through giving it the elements:
int[][] rectangular = new int[] {
	{1, 2, 3, 4},
	{5, 6, 7, 8},
}; // remember the semicolon
```

*Trick Question*: The inner rays DO NOT HAVE TO BE THE SAME SIZE. For example:
```java
int[][] ragged = new int[] {
	{1, 2, 3, 4},
	{5, 6, 7},
	{8, 9, 3, 4, 5}
}; // remember the semicolon
```
#### EXTREMELY IMPORTANT: Aliasing: Array Shallow vs Deep Copy
Shallow copy - **same reference**, **same references in array**

> [!danger] SHALLOW COPYING IS DANGEROUS!
> 
> As seen in the example below, forgetting about shallow copying will result in unintended changes to original arrays! This **WILL** be something that can easily mess you up on the exam if you aren't actively thinking about it! 

```java
int[] nums = {1, 2, 3, 4};

// THIS IS A SHALLOW COPY.
// If you modify shallowCopy, you are ALSO modifying nums
int[] shallowCopy = nums;

shallowCopy[2] = 20;

// nums        == { 1, 2, 20, 4 }
// shallowCopy == { 1, 2, 20, 4 } 
```

##### Deep Copying
To **deep copy** an array, 
1. Create a new array (to prevent aliasing)
2. Deep copy each element in the array

- Primitives - **NO** distinction between shallow and deep copy (there are no references)
```java
int i = 3;
int b = i; // this is deep copied -- it isn't a reference to i 
```

- Immutables - e.g. String - can be shallow copied since they are **immutable**

Reasoning: If I have an object that is considered immutable, its value cannot be changed. As a result, there isn't a fear of some shallow copy modifying it (because it can't be modified by anything). 

> [!reminder] String Immutability Reminder
> Strings are **IMMUTABLE**! Take a look at the following: 
> 
> ```java
> String s = "bob";
> String b = s; // s is immutable, this is NOT a shallow reference (you're safe to modify it) 
> ```


![[Pasted image 20231016163602.png]]


### Pass-by-Value

**JAVA IS PASS-BY-VALUE!!!**

When you pass a variable into a method, it will **always** copy the variable. 

**However**, if it is a type of object (reference type), it is only **copying the reference**, NOT the values. This is what results in *Shallow Copying*.

```java
public static void main(String[] args) {
	int[] arr = { 1, 2, 3, 4 };

	// THIS IS ALSO MODIFYING THE "arr" IN THIS SCOPE!!!!
	int[] returnedArr = modifyArray(arr);

	// Output:
	// Notice arr[0] was changed!
	// arr == { 11, 2, 3, 4 };
	// returnedArr == { 0, 0, 0 };
}

public static int[] method(int[] arr) {
	if (arr[0] > 0) {
		arr[0] += 10; 
	}

	// T
	arr = new int[3];
	return arr;
}
```

### (IMPORTANT) Check Style Guide
To run:
```sh
java -jar [path to checkstyle jar] [path to .java file]
```

Example:
```sh
java -jar checkstyle.jar TestClass.java
```

**USING CHECKSTYLE WITH JAVADOCS ONLY**:
```
java -jar -j checkstyle.jar 
```

**USING CHECKSTYLE WITH STYLE + JAVADOCS**
Think of "-a" stands for checking "all"
```
java -jar -a checkstyle.jar TestClass.java
```

# Recitation 6

### Classes
**Class**: *blueprint* that an **object** can be created from 

- We call the actual object an **instance** of the class

- There can be several objects of one class, each with its own data
![[Pasted image 20231018000021.png]]

- **instance fields** - describe state of the object
- **instance methods** - behavior of an object 

The following would be **instance fields**:
**Data**: double stringLength, double radius

The following would be **instance methods**:
**Methods**: yoyo(), wrapUp()

##### Instance Fields

![[Pasted image 20231018000416.png]]

- Describes state of **specific** index
- Each instance has its own data
- data should be **encapsulated** (other things shouldn't be able to modify it without a getter or a setter) to protect its data
- Instance fields have a **default** value (*This might be null!*)

##### IMPORTANT: Static Fields
- Belongs to **class**, NOT specific instance 
- **shared** by each instance
- If field is modified, the value is modified for **all instances**

Examples of when to use static?
- *Constants (static final)*
- Counter

Useful chart showing default values:
![[Pasted image 20231018000829.png]]

##### Instance Methods
- Describes **behaviors or actions**
- **must** be called on instance of the class

*Trick Question:* If you are in a **static method**, you CANNOT call an instance method:

```java
public class Student {
	private String name;

	public String getName() {
		
	
	}

	public static void someStaticThing() {
		System.out.println(getName()); // This throws a COMPILER ERROR, as getName() is an instance method!
	}
}
```

**Getters and setters** - common instance methods that set/get a field in a class
- We use getters and setters to restrict what outside things can do
- This is extremely useful if we want to do some sort of check of the value *before* the value is set!

*Trick Question*: Even though static methods cannot access instance methods or fields, instance methods **can** access static methods and fields.

```java
public class Yoyo {
	private YoyoColor color;

	public void setColor(YoyoColor color) {
		this.color = color; 
	}
}
```

##### Static Methods
- uses `static` keyword 
	- `public static int myMethod(int parameter) { ... } `
- NOT in respect to an instance
- CANNOT access instance data

```java
Car c1 = new Car();
//Assuming getCarCount is a public static method:

Car.getCarCount(); // preferred
c1.getCarCount(); // still works, but not recommended
```

### Instance fields vs static fields
![[Pasted image 20231018002936.png]]
### Visibility modifiers
The main visibility modifiers section can be found in a later recitation in this document.

Main points from recitation 5:
- Determines **accessibility** of your code

4 types: public, private, protected, default (SEE DIAGRAM IN LATER RECITATION) 
### Encapsulation
- protect data by making variables private by default
- values can **only** be changed through public methods (forcing protection)

Why encapsulate?
- **Flexibility** - easier to change code
- **Maintainability** - easier to change other parts without breaking

##### Getters ("accessor methods")
- gets value, naming convention starts with get
- has a return type
```java
private double stringLength;  

public double getStringLength() {  
	return this.stringLength;  
}
```

##### Setters ("mutator methods")
- sets value, naming convention starts with set
- often uses `this` to avoid shadowing
- usually doesn't return anything

```java
private String owner;

public void setOwner(String owner) {
	this.owner = owner;
}
```

### Constructors
- Initializer for a class
- **NO RETURN TYPE, NOT EVEN VOID**
- Typically assigns passed in values to instance fields

```java
public class Yoyo {
	private double stringLength;
	private double radius;
	private YoyoColor color;
	private String owner;

	public Yoyo(double stringLength, double radius, YoyoColor color, String owner) {
		this.stringLength = stringLength;
		this.radius - radius;
		this.color = color;
		this.owner = owner;
	}
}
```

### `this` keyword, other reserved keywords
- Refers to the **current instance** of the class

Why use `this`?
- Specify instance field instead of local variable (**AVOIDS SHADOWING**)
- Constructor chaining (seen later)
- Reference current instance

```java
private String color; // instance field

public Yoyo(String color) { // local variable
	this.color = color;
}
```

*Trick Question that WILL be on the exam:* If you **forget** the `this` part, it will ONLY set the local variable to itself, doing nothing!!!!

```java
private String color;

public Yoyo(String color) {
	color = color; // this is setting the local variable, NOT what we want
}
```

##### Default Constructors
- Java by default has an **empty default constructor**
- Default constructor **no longer exists** if you create a new one

```java
public class Yoyo {
	public Yoyo(String color) {
		// ...
	}
}

Yoyo yoyo = new Yoyo(); // THIS NO LONGER WORKS, AS WE NOW HAVE ONLY 1 CONSTRUCTOR REQUIRING A COLOR!
```

##### (IMPORTANT) Constructor Overloading
- You can overload constructors to offer multiple different parameter choices:

```java
public Yoyo(double stringLength, double radius, YoyoColor color) {  
	this.stringLength = stringLength;  
	this.radius = radius;  
	this.color = color;  
}  

public Yoyo(YoyoColor color) {  
	this.stringLength = 40;  
	this.radius = 1;  
	this.color = color;
}
```

##### (EXTREMELY IMPORTANT) Constructor Chaining
- Constructor chaining saves code
- **Goes from lesser arguments to more arguments**
- Uses `this` to reference another constructor

Take this example:
```java
public Yoyo(double stringLength, double radius, YoyoColor color) {  
	this.stringLength = stringLength;  
	this.radius = radius;  
	this.color = color;  
}  

public Yoyo(YoyoColor color) {  
	this.stringLength = 40;  
	this.radius = 1;  
	this.color = color;
}
```

If using constructor chaining:
```java
public Yoyo(double stringLength, double radius, YoyoColor color) {  
	this.stringLength = stringLength;  
	this.radius = radius;  
	this.color = color;  
}  

// This has less arguments, so it uses one with more arguments
public Yoyo(YoyoColor color) {  
	this(40, 1, color);
}
```

##### Reserved Keywords
`static` - defined at class level; belongs to class itself

`null` - default value for reference types; NO object/instance assigned to it 
- If you try to access a field or method of a null object it will throw a **NullPointerException**

*Very Useful Tip*: Often **short circuiting** will be used for null checks!
```java
Student s = null;

// the first part prevents the null pointer exception from .getName()
if (s != null && s.getName().equals("Sal")) {
	// ...
}

```

Person s = new Student();

```java
public double getGrade() {
	return 0.0;
}

int grade = (int) getGrade();
```

((Student) s).doHomework();

(the meme is hardly relevant, but I love seeing it every few years)
![[Pasted image 20231018004650.png]]
# Recitation 7

### Aliasing - Shallow vs Deep copy (again)
Aliasing = an **Object** has multiple aliases

What is an alias?
```java
String s1 = new String("some string");
String s2 = s1; // This is saying "s2 is now an ALIAS of s1" s1 and s2 are the same reference to the same object

System.out.println(s1 == s2); // Because the references are the same, this is true

int[] a1 = {1, 2, 3, 4};
int[] a2 = a1; // This is aliased and is a SHALLOW COPY!!!

a2[1] = 3; // THIS WILL MODIFY a1
// a2 == { 1, 3, 3, 4 }
// a1 == { 1, 3, 3, 4 }
```

### Shallow copy array
##### Shallow copying
*Trick question*: Even though we typically have a loop like this to deep copy, because the array has **objects** it is actually shallow copying!
```java
Yoyo redYoyo = new Yoyo(38.0, 1.25, "red", "Lucas");
Yoyo blueYolo = new Yoyo(40.0, 1.0, "blue", "Allison");

Yoyo[] arr = new Yoyo[2];

arr[0] = redYoyo;
arr[1] = blueYoyo;

Yoyo[] copy = new Yoyo[arr.length];
// Array is NOT shallow copied, but the objects inside each array is! 

for (int i = 0; i < copy.length; i++) {
	copy[i] = arr[1]; // shallow copying Yoyo objects
}

arr[0].setColor("yellow"); 

System.out.println(copy[0].getColor()); // Prints yellow
```

Useful recitation diagram:
![[Pasted image 20231017211600.png]]

##### Deep copying
**Deep copy** - create **new** identical instance (AND its fields) to avoid aliasing shown above
- If an instance field is a **reference**, if you don't deep copy it **will** shallow copy

**Copy constructor** - Constructor that creates a deep copy 

Verbose way:
```java
public Yoyo(double stringLength, double radius, String color, String owner) {
	this.stringLength = stringLength;
	this.radius = radius;
	this.color = color;
	this.owner = owner;
}

public Yoyo(Yoyo other) {
	// We are copying every field of another yoyo to this object
	this.stringLength = other.stringLength;
	this.radius = other.radius;
	this.color = other.color;
	this.owner = other.owner;
}
```

Constructor chaining way (**RECOMMENDED**):
```java
public Yoyo(Yoyo other) {
	this(other.stringLength, other.radius, other.color, other.owner);
}
```

Example usage:
```java
Yoyo yoyo = new Yoyo(35.5, 2.5, "Red", "Alex");

// This is a DEEP COPIED Yoyo and is completely separate
Yoyo secondYoyo = new Yoyo(yoyo);
```


Now we can take the previous example to deep copy using this new constructor:
```java
for (int i = 0; i < copy.length; i++) {
	copy[i] = new Yoyo(arr[1]); // DEEP copying Yoyo objects
}
```

### Wrapper classes
Think of one of these candy wrappers:
![[Pasted image 20231017215729.png]]

The wrapper is **wrapping** around whatever candy might be inside. You still have that exact same candy, but wrapper could also have something like a label on it, color, etc. and overall **encapsulates** (surrounds) whatever it is a wrapper for.

- They most often are surrounding **primitives**:
**ALL WRAPPERS FOR PRIMITIVES ARE IN java.lang AND DO NOT REQUIRE IMPORTING**
byte --> Byte
short --> Short
int --> Integer
long --> Long
float --> Float
double --> Double
char --> Character
boolean --> Boolean

- You **CAN** call methods on a wrapper class (as it is an Object!)


##### IMPORTANT: Autoboxing / Autounboxing
Java will **autoconvert** between primitive types and wrapper types when needed

*Tip* - Think of boxing as literally putting something inside of a box, whereas unboxing is taking out 

**Autoboxing** - autoconverts primitive to wrapper
```java
// Notice the type has a capital letter to signify wrapper!
Double doubleWrapper = 5.0; // 5.0 is a primitive, but gets autoboxed into a wrapper
```

**Autounboxing** - autoconverts wrapper to primitive

```java
double primitiveDouble = doubleWrapper; // doubleWrapper is a wrapper type, but gets autounboxed to primitive
```

*COMMON QUESTION - Is autoboxing, autounboxing, or both occurring in the following code?*
```java
Integer num1 = 5;
Integer num2 = 3;

int sum = num1 + num2;
```

ANSWER: BOTH! Integer declarations are being autoboxed into wrappers, but the sum is a primitive, requiring num1 and num2 to be autounboxed.


#### Useful Wrapper Methods
**parseInt** - Converts String to int 

```java
String someNum = "348";

// Note that Integer was the wrapper class!
int num = Integer.parseInt(someNum);

// num == 348
```

```java
String s = String.valueOf(3498);

String s = 3498 + "";

// s == "3498"
```

### Inheritance

Extending a class: "**is a**" relationship

**Parent Class** - "superclass"; class being extended from

**Child Class** - "subclass"; class extending from parent class

Subclass will **inherit** all information from parent, INCLUDING methods!
- Inheritance will ONLY occur when a field or method is **public** or **protected**

> [!reminder] Protected is for same package or a subclass.

Why use inheritance? Code reuse, and **reducing repetition**

How to use inheritance?

`extends` - inherits from the class on the right 

```java
// Yoyo is extending Toy
// Yoyo "is a" Toy
public class Yoyo extends Toy {
	// Code
}
```

*Trick Question:* You **cannot** extend a class marked as `final`.

#### Class Hierarchies
- *Seen as exam question!* Every object extends from Object, but **not necessarily explicitly**

![[Pasted image 20231017225806.png]]

`FirstYear` **does** extend Object, but it is considered **implicitly** because it goes through several other classes before reaching that point. On the other hand, `Person` is **explicitly** extending Object.

### Javadocs
- Special comments to describe a class, field or method
- **Describes functionality**, and gives extra information
- Helps other people understand your code (and future you)
- Uses tag annotations for specific attributes:

`@author`: author of whatever it's describing
`@version`: version of whatever it's describing
`@param`: a parameter of a method; format: `@param <paramName> <description>`
`@return`: what a method might be returning 

NOTICE: Javadocs begins with `/**` and ends with `*/`, but the `*` for each line is optional!

Example:
```java

/**
*
* Adds two integers together as per the + operator.
*
* @param a the first operand
* @param b the second operand
* @return the sum of a and b
*/ 
public static int sum(int a, int b) {

}
```

### Packages
Packages - group classes together 

##### Creating package
- Create folder that is the name of the package
- Place all classes you want in that package
- Write `package <folder.name>` at the top of each class in the package
- Java must know the path of the packages, by default goes into current working directory 

> [!note] On the topic of packages
> Although you need to understand what packages **are**, you are not required to ever create one in this course.

### More visibility modifiers (protected/default)

Protected:
- accessible to **subclasses** (regardless of package), and **all classes in same package**

Default (no visibility modifier):
- known as "package-private"
- **accessible to all classes in same package**
- Subclasses only inherit default IF in the same package as superclass
![[Pasted image 20231017230553.png]]

### Overriding
Subclass can **override** a method from its parent class

- *SEEN IN EXAM QUESTIONS* SAME name and SAME parameters, but DIFFERENT implementation

##### @Override annotation
- @Override is **not** required, but will allow the compiler to throw a **compile error** if there was an improper override
- @Override is **not** what overrides a method

*Exam Question* You **CANNOT** override `static` or `final` methods.
![[Pasted image 20231017231001.png]]
# Recitation 8

### Components of a good class (equals, toString, hashCode)
3 main methods you often override from Object:

`equals()`

`toString()`

`hashCode()` - *YOU DO NOT NEED TO OVERRIDE OR WRITE THIS FOR THE EXAM, BUT YOU HAVE TO KNOW WHAT A HASHCODE'S FUNCTIONALITY IS*

##### (EXTREMELY EXTREMELY IMPORTANT) equals() overriding
- Default equals() is *reference equality*
- Override equals() for *value* equality

The `equals()` method requires **5** rules:
- **Reflexive** - x.equals(x) == true
- **Symmetric**: x.equals(y) == y.equals(x)
- **Transitive** if x.equals(y) == true and y.equals(z) == true, x.equals(z) == true
- **Consistent**: If no object data modified, x.equals(y) always returns same result
- **Comparison with null**: x.equals(null) returns **false**
![[Pasted image 20231018010528.png]]


##### toString()
By default returns the following:

```java
public String toString() {
	return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

Our potential override:

```java
@Override // REMEMBER: @Override not strictly needed, but recommended
public String toString() {
	return String.format("My name is %s and I am %d years old.", name, age);
}
```

##### hashCode()
*YOU DO NOT NEED TO KNOW HOW TO IMPLEMENT A HASHCODE*

- Returns an **integer** representation of an object

Requires the following rules:
- **Consistency** - if object is not modified, hashcode will remain same
- If two objects are **equal**, they have the **same hash code**
- If two objects have the **same hash code**, they are NOT necessarily equal

### Abstract classes
- **CANNOT** be instantiated
- Used to define the common states and behaviors of subclasses
- Denoted by `abstract` keyword
- "Template" where abstract methods HAVE to be implemented by a concrete class

**Concrete class** - non-abstract

If the answer is "it depends" it probably is abstract.

Example: I have a Shape class. What is the area of a Shape?

Answer: It depends. As a result, Shape could very easily be an abstract method:


```java

public abstract class Shape {]
	public abstract double getArea(); // This would have to be implemented by any concrete class extending it
}

public abstract class Square extends Shape {
	// getArea HAS to be implemented as it was abstract
	@Override 
	public double getArea() {
		// ...
	}
}

```

Other properties:
- Abstract methods
	- no implementation needed
	- **MUST** be overriden when inherited by a **concrete** class
		- cannot be `private` - private isn't visible
		- cannot be `static` - static cannot be overriden
		- cannot be `final` - final can't be overriden
- **can still have constructors, non-abstract methods, and instance vars**

Recitation Example:
![[Pasted image 20231018011355.png]]


Why abstract?
- Reuse code
- Not every object needs to be instantiable
	- No point in declaring a Shape, it doesn't have an area!
``

### Polymorphism
![[Pasted image 20231018011447.png]]

- Object can behave differently based on context

**Static Type** - type of reference at *compile time*
- What the compiler knows the object is for sure
- Determined when the variable is declared, **NEVER** changes

**Dynamic Type** - type of reference at *runtime*
- What the object *actually is*
- Dynamic type **may change via assignment** 
- Dynamic type will **always** have a "is a " relationship
	- A Person "is-a" Person, a Student "is-a" Person, etc.

> [!tip] Polymorphism Practice
> Make sure to check the recitation slides for polymorphism practice!

```java
Person p1 = new Student();
p1.study();
```
- Static type is Person (the type on the left)
- Dynamic type is Student (set on the right)
- Valid because Student "is-a" Person

At compile time:
- Java checks if Student is a Person (good in this case)

At runtime:
- Java checks the implementation provided by the dynamic type
- if `study()` is in both Student and Person, then it will run the `Student` method! 


##### Casting Precedence
![[Pasted image 20231018011945.png]]


What does casting do?
- Changes the **static type** of the reference

```java
Person p1 = new Student();

// We are changing the static type of the reference from Person to Student
Student s = (Student) p1;
s.getAge();

// NOTE: The above code is equivalent to this shorthand:
((Student) s).getAge();
```

**Upcasting** - cast to supertype; *Always compiles and runs*
```java
Student s1 = new Student();

Person p = (Person) s1;
```

**Downcasting** - cast to a subtype; *Always compiles, SOMETIMES runs*
```java
Person s1 = new Student();

// This MIGHT fail if s1 isn't actually a type of Student
Student s = (Student) s1;
```


**Sidecasting** - Casting to neither a supertype nor subtype
```java
Shampoo shampoo = new Shampoo();
Gloves gloves = new Gloves();

// Obviously not the same type, won't compile, never runs
Shampoo s = (Shampoo) gloves; 
```