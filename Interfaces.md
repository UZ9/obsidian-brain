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
