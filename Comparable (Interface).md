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
