### Exceptions
- Occur during **runtime** -- "disruption of code"
- Method creates a new **Exception** object, and hands it to the **JVM** if you `throw` it
- Extends from **Throwable** class
	- "Throwing an exception" = creating exception, handing it to JVM

> [!important] Know the difference between checked and unchecked exceptions! 

**Checked exceptions** - checked at compile time 
- NOT subtype of `RuntimeException`
- **MUST** be caught using a `try` statement or acknowledged by declaring in the `throws` clause of method header
- If not caught, causes a **compile rror**
**Unchecked exceptions** (runtime exceptions) - only fails at runtime
- Extends `RuntimeException`
- Typically not reasonably expected to check for these exceptions
	- 3 / 0 will throw a RuntimeException, but would you really want to `try catch` every single time you divided two numbers?
- If not caught, causes a **runtime error**

Checked exceptions -- REQUIRES `try {} catch {}` statements (or adding `throws` to the method header)
![[Pasted image 20231107105751.png]]
##### Exception Response Options
- Do nothing, let the program crash
	- NOT allowed for checked exceptions
- Handle exception immediately with `try` statement
	- Code that potentially throws the error is contained in a `try` block
	- The correct exception is caught in the `catch` block
- Let exception *propagate* to another
	- Add `throws` to method header 

Keywords `throw` and `throws`
- `throw`: Hands an exception over to the JVM 
	- If the exception is a checked exception, it MUST be caught
- `throws`: Used for exception propagation (let another method deal with it)

> [!important] **CREATING AN EXCEPTION IS NOT WHAT CAUSES THE ERROR, ONLY WHEN YOU THROW IT!** 

Example:
```java
public static void main(String[] args) throws Exception {
	n = 2;

	if (n == 2) {
		// Create new exception and throw it (hand off to JVM)
		throw new Exception("Something went wrong");
	}
}
```

Result:
```
Exception in thread "main" java.lang.Exception: Something went wrong
	at Test.main(Test.java:6)
```

##### Method Propagation
- Every method has two options: try catch an exception, or "hand the exception" over to something else
- If the method *does not* handle the exception (and uses `throws`), the method is **propagated** to another method
- If no method handles the exception (e.g. you add `throws` to public static void main), the JVM will default to printing the **stack trace** (where the error happened) and the name of the exception
- CHECK LIST EXCEPTIONS IN THE THROWS CLAUSE!
##### Try Catch Statements
**try block** - code that potentially throws exception

**catch block** - code executed when a particular exception is caught

**finally block** - ALWAYS executes, EVEN if catch block throws an exception
- Useful for things such as closing a Scanner properly even if there was an error

```java
public static void main(String[] args) {
	try {
		System.out.println(4 / 0);
	} catch (ArithmeticException e) {
		System.out.println("ArithmeticException caught!");
	} catch (Exception e) {
		System.out.println("Generic exception caught!");
	} finally {
		System.out.print("Done!");
	}
}
```

Result: `ArithmeticException caught! Done!`
>[!warning] Two catch blocks will never fire in the same `try catch` block.
>The code will attempt to go to the very first exception that fits the description (in this case ArithmeticException checked out and was first), and WOULDN'T execute the `Exception e` portion.