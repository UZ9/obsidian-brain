[[010 CS1331 MOC]]
# Recitation 9

### Interfaces 
Interfaces = "this class **does** this thing"

> [!info] "Word" difference between `interface` and `abstract`
> One way to think about abstract vs interface is abstract is used for "**is a**" behavior, while interfaces are used for "**does**" behavior." Example: Square is a Shape (Shape is abstract), a person is Interactable (interface, does interaction).

- Most commonly seen with `able` suffix
	- e.g. Compar**able**, Spread**able**

- Methods **can** be static
- Methods **can** have `default` methods (default implementation)
- The **only** fields you can have an interface are constants (static final)
	- You do **NOT** have to mark them as static final (compiler will do it automatically)
- **CANNOT** have any instance fields nor constructors

Pay **VERY** close attention to the following example:
```java
public interface Spreadable {
	// Even though it isn't marked, because it's an interface GRAMS_PER_TBSP is public static final 
	double GRAMS_PER_TBSP = 14.79;

	// default method = public abstract
	// a concrete class would HAVE to implement spread
	void spread();

	// Default methods CAN have implementation
	default void taste() {
		System.out.println("Tasting");
	}
}

public class PeanutButter implements Spreadable {
	public void spread() {
		// You HAVE to specify GRAMS_PER_TBSP is part of the interface!
		System.out.printf("Spreading %.2fg of peanut butter!", Spreadable.GRAMS_PER_TBSP)
	}
}
```

##### Extending Interfaces
- Interface extends another interface using `extend`
- Similar to abstract classes--a concrete class has to implement **ALL** abstract methods

> [!Warning] Abstract/Interface Trick Question
> Although a **concrete** class has to implement all methods, if an **abstract class or interface** extends another interface it **does not** have to override the abstract methods!
> 
> This was similar to the scenario where you had an abstract class extending another abstract class.

Example of interface extending interface:
```java
public interface Eatable {
	void eat();
}

public interface Spreadable extends Eatable {
	// Because Spreadable is an interface, it DOES NOT have to implement eat
	void spread();
}

public class Jelly implements Spreadable {
	// Jelly is forced to implement BOTH abstract methods (eat, spread)
	public void eat() {
		System.out.println("Eating jelly");	
	}

	public void spread() {
		System.out.println("Spreading jelly!");
	}
}
```


A **functional interface** is an interface with **one** abstract method.

Example:
```java
public interface Eatable {
	void eat(); // One abstract method = "functional interface"
}
```

An interface **can** be the static type of a variable.

Example:
```java
public interface Eatable { 
	//... 
}

public class Hotdog implements Eatable {
	// ...
}

// Static type Eatable, because Hotdog is Eatable
Eatable eatable = new Hotdog();
```

##### Abstract vs Interface Diagram
![[Pasted image 20231102155328.png]]

### Comparable (Interface)
A class that implements `Comparable` can be **compared** to other objects (usually same type)

- Often used for sorting objects ("I need to know whether this HotDog is considered 'greater' than another HotDog")

Examples of Comparables:
- `String`, `Integer`, `Double`

**Not all** classes implement `Comparable`! 
 
IMPORTANT: Test will have a question in which a recursive method has no exit, resulting in `StackOverflowError`

##### How does Comparable work?

Comparable has one abstract method:
```java
// T is what will later be discussed as a Generic--it's a way for the compareTo to actually compare something of the same object (e.g. a HotDog would compareTo a HotDog).
// The nice benefit of this is there is no casting involved (as opposed to equals, which takes in an Object)
public int compareTo(T other);
```

Return value of `x.compareTo(y)`:
- A **negative** integer if **x** is **lesser** than **y**
- A **positive** integer if **x** is **greater** than **y**
- **0** if **x** is considered **equal** to **y**
	- Strongly recommended that compareTo is equivalent to equals, but not explicitly required


##### Comparable Example
```java
// Comparable has <> (part of generics, you'll learn it soon) where inside of the brackets a type must be specified to compare to.
// In this case, Dog can be compared to Dog
public class Dog implements Comparable<Dog> {
	private int age;

	// CONVOLUTED IMPLEMENTATION:
	// Because Dog implements Comparable<Dog>, compareTo will take in a Dog as an input
	public int compareTo(Dog other) {
		if (this.age > other.age) {
			return 123_456; // Does NOT necessarily need to be 1, but positive represents "greater"
		} else if (this.age < other.age) {
			return -1_331; // Does NOT necessarily have to be -1
		} else {
			// Age must be equal, return 0
			return 0;
		}
	}

	// SHORTENED IMPLEMENTATION (note you would only have one of these methods, but both are shown here as an example)
	public int compareTo(Dog other) {
		// Example: this age is 3, other age is 2, 3 - 2 = 1
		// therefore, this dog is greater than other dog

		return this.age - other.age;
	}
}
```

### ArrayList
### Generics -- Basics
### Asymptotics/Big-O
### Searching
### Sorting 

# Recitation 10
### Exceptions
- Occur during **runtime** -- "disruption of code"
- Method creates a new **Exception** object, and hands it to the **JVM** if you `throw` it
- Extends from **Throwable** class

**Checked exceptions** - checked at compile time 
**Unchecked exceptions** - fails at runtime

Checked exceptions -- REQUIRES `try {} catch {}` statements

##### Try Catch Statements

# Recitation 11