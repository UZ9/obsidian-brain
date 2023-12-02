Recursion = method calling itself

**3 components**:
- **Base case** - "smallest problem" -- what ends a recursive method, and typically has the easiest solution; YOU CAN HAVE MULTIPLE BASE CASES
- **Recursive calls** - solves another problem
- **Approach a base case** - decrease problem size to eventually get to a base case
	- Stops infinite recursive calls

##### Simple Example - Calculating Factorial
```java
public static int factorial(int n) {
	// BASE CASE
	if (n == 0) {
		return 1;
	}

	return n * factorial(n - 1);
} 
```

**base case** - n = 0, n = 1
**recursive call** - find factorial of $n - 1$
**approaching base case** - finding the factorial of a smaller number

##### Loop Conversion
If you wanted the equivalent of a loop in recursion:

For loop:
```java
for (int i = 0; i < 10; i++) {
}
```

Equivalent recursion:
```java
public static void recursiveLoop(int i) {
	if (!(i < 10)) return;

	// Do whatever code

	recursiveLoop(i + 1);
}
```