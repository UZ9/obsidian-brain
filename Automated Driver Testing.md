[[Main Driver]]

Written by Ryder Johnson, 11/3/23

![[Pasted image 20231103190623.png]]
### Introduction
CS1331 Homework assignments can be quite unforgiving. From what feels like hundreds of possible constructors to the many, *many* edge cases, the tests required for each component has exponentially increased with every week--with a desperate need for a streamlined process.

When I initially got together with Justin for HW4, we identified the issues plaguing older iterations of our drivers, and came up with the following restrictions:
- **Portable** - Arguably the largest (and most painful) limitation: everything must be in a single `.java` file. The end user should be able to directly drag the file into their project with no other requirements, leading to the unfortunate complications of:
	- **No more than one file** - EVERYTHING must be contained in a single `.java` file for distribution.

	- **No outside dependencies** - No JUnit, Mockito, Selenium, etc. to use for easy test creation. As seen later on in this article, we essentially wrote our own variant of JUnit.

- **Robust Tests** - Tests must be easy to create, easy to read, and easy to modify if needed.
	- **Feedback-based System** - The tests should notify the developer of specifically *what* they missed, along with the stack trace of where it might have occurred. 

	- **Exception Handling** - All sorts of exceptions (some intentional) can be thrown from the end user's code. In order to prevent this from breaking the entire testing environment, these are caught and internally handled. 

	- **"No clutter nonsense"** - Tests should be as clear and intuitive to read as possible, requiring a few terminal tricks for formatting. 

### The problem of portability
The HW5 driver totaled **1984** lines of code. Having a file anywhere near this size is borderline *impossible* to maintain--not to mention it brings even more complications:

What if we had 20+ features where each one would typically have its own class?

If you write to a file and I want to check it against an expected output, what if there was 60+ lines? Do I have to manually write out a String with a billion `\n` characters?

##### Solving the class problem
This was the very first issue we addressed, and through its iterations has been the sole reason maintaining this project has feasible whatsoever.

The whole point of object oriented programming is in its name: *using objects*. It seems fairly ironic when you're only working with one file and class--right?

...but does it have to be one class?

Let's take a look at the Java specification documentation, specifically [§6.6.2](https://docs.oracle.com/javase/specs/jls/se8/html/jls-6.html#jls-6.6.2 "6.6.2. Details on protected Access"):

> [!important] If a class lacks the `public` modifier, access to the class declaration is limited to the package in which it is declared ([§6.6](https://docs.oracle.com/javase/specs/jls/se8/html/jls-6.html#jls-6.6 "6.6. Access Control")). In the example:
> 
> ```java
> package points;
> public class Point {
>   public int x, y;
>    public void move(int dx, int dy) { x += dx; y += dy; }
>}
>class PointList {
>    Point next, prev;
>}
>```
>two classes are declared in the compilation unit.

Or in other words: **we can put as many non-public classes into one file as we want**.

That's all fine and dandy, but how does that solve dealing with massive driver lengths? 

Because we're able to store multiple classes in one file, it *also* means we could work in multiple files our end, and have some sort of **script** automatically squash them into one for distribution.

##### The problem with imports
If you were to directly append all `.java` files, you would run into 3 issues:
1. **Multiple classes with public visibility** - If we were writing `public class ...` in our individual files, this would result in an error when combining. A solution to this was simply search for the visibility modifier of a class and if it exists, remove it. 
2. **Imports not at the top** - Java requires **all** imports to be at the top of a file, where simply appending would result in imports being scattered throughout.
3. **Duplicate imports** - Duplicate imports throw a compiler error, and is unfortunately something to account for. If two classes happened to use ArrayList, two ArrayList imports would show up in the resulting Driver file

To solve the last two issues, the script initially used the following methodology: 
```
<RESERVED_IMPORT_SPACE>

<CODE_LINES>
```

1. Pass through the entire `src` directory and glob all `.java` files
2. If the class is marked as `public class`, remove the visibility modifier
3. For each line, if it happens to be an import statement add it to a special reserved import space container 
4. If the line happens to be code, add it to the code lines list 
5. At the end of parsing all `.java` files, write to `Driver.java` using the schema shown above 

This ended up working perfectly! ...for HW4 and HW5.

##### (as of HW6) Data files 
As I mentioned above, the second issue was being able to store relevant `.txt` files on our end to cross reference a test's output, e.g. a `PrintWriter`. Once again, the issue is that we *can't* distribute text files. 

Another problem is how we locally run the driver code. We don't use the python script to run the driver when developing it, meaning you have the following scenario:

- The driver needs to have the contents of the `.txt` file--sure, we could dump the contents of it during the python script.
- Running it locally *also* needs to have access to the `.txt` file--making this not quite as simple.

To answer this problem, I have to first introduce you to how tests are written.

### But what does a test look like?
Take a look at the following example of a test:
```java
    @TestCase(name = "Testing that all 7 genres exist in the correct order...")
    @Tip(description = "\nHow many genres should there be? What order should they be in?")
    public void genresExistInCorrectOrder() throws TestFailedException {
        String[] correctGenres = new String[] {"ACTION", "COMEDY", "FANTASY", "HORROR", "MYSTERY", "ROMANCE", "SCI_FI"};
        Genre[] genres = Genre.values();
        for (int i = 0; i < 7; i++) {
            TestFunction.assertEqual(genres[i].toString(), correctGenres[i]);
        }
    }
```

The following was a check for the `Genre` class implemented in HW5 containing all of the correct genres, in the correct order.
##### Custom Java Annotations
Remember `@Override`? This is an example of a **Java Annotation**, where either a method, class, or field can be marked with a special "tag" of information for later use during runtime. Here's a brief description of our current annotations:

- `@TestCase` - Used for denoting the following method is a test. Takes a `name` field for describing the intent of the test (we show this to the user)
  
- `@Tip` - If a test fails, we provide a message providing a potential cause as to why their code might've failed (without getting too specific).

New annotations arriving for HW6:
- `@BeforeTest` - Used for common code ran between all tests in a class (e.g. for static classes we have a reset method run before every test)

- `@AfterTest` - Runs after the test, usually for static classes requiring some sort of cleanup function
  
- `@InjectData` - Injects data from `.txt` and inserts it into a String. This ended up being a massive change **and is the secret sauce to data files**.

##### Test Functions
In order to actually **assert** whether some sort of snippet has passed or not, we need some sort of way of comparing a multitude of different values, while using that to determine whether a test has been passed or not.

To do this, we utilize custom Test exceptions thrown when a test fails:
```java
// Strings are different values, throw exception
throw new TestFailedException("Strings different! Received " + actualString + " but expected " + expectedString);
```

These are then caught later and processed as either failed or passed tests. More on that later!

### Back to data files
Now that Java Annotations have been roughly explained, we can go back to the implementation of data files.

Example scenario: The user has code that needs to be tested. The code does the following:
1. Counts from 1 to 10 and puts this into a `List<Integer>`
2. Uses a `PrintWriter` to write this to `Numbers.txt`

The main test case for checking whether the user has successfully put in the correct numbers would be retrieving their output using a `Scanner`, and comparing it to the expected values.

However, this can be incredibly cumbersome if we had to write this in a String, similarly to our other test cases:
```java
// This is terrible.
String expectedOutput = "1\n2\n3\n4\n5\n6\n7\n8\n9\n10";
```

Instead, what if we had a way of keeping our own `TestData.txt`, and we were able to compare their output to that text file? Recall we have the single file issue, so this would have to be streamlined in some way.

Enter: The new `@InjectData` annotation:
```java
class TxtTestData {
    @InjectData(name = "TestData.txt")
    public static String DATA = "";
}
```

`TxtTestData` is an example of what I now call a **Data class**. A data class is a class explicitly registered to the `TestManager` (we'll get to it, don't worry) that contains one or more data inputs (we might rename `@InjectData` to `@DataInput`, not too sure yet)

The `TestManager` allows a data class to be registered using the following method:
```java
public static void registerDataClasses(Class<?>... classes);
```

During runtime, it does the following:
1. For each data class, scan for all fields with the `InspectData` annotation
2. For each field, enforce public visibility, and start a new Scanner with the path being `name`
3. Loop through and convert the scanner's output to a single string with `\n` delimiter 
4. Replace the value of the field with the scanned output--in the example above, `DATA` would be set to whatever contents `TestData.txt` contained 
5. Run the tests with the new pulled data

This now allows us to *really* easily compare test cases to a `PrintWriter`: 
```java
TestFunction.assertEqual(output, TxtTestData.DATA);
```

where `DATA` would be populated using Reflection (more on that in the Reflection section).

##### That still doesn't solve the one file issue 2: Electric Boogaloo
...because there's always something else!

The issue is that if we export this to a single `.java` file we quite literally cannot export a `.txt` with it--as that would be violating one one of our restrictions.

Just a tad ago I mentioned this was really bad to write:
```java
// This is terrible.
String expectedOutput = "1\n2\n3\n4\n5\n6\n7\n8\n9\n10";
```

...but what if we ALSO got the python script to do this for us?


```
class TxtTestData {
    @InjectData(name = "TestData.txt") <-- InjectData found with "TestData.txt", signal injection
    public static String DATA = ""; <-- Injection prepared, fire injection sequence into DATA
}
```

The process is more or less the following:
1. While parsing each line in a `.java` file, attempt to find a line with the `@InjectData` annotation
2. If the `@InjectData` annotation is found, override default behavior and parse the value between the quotation marks using regular expressions 
3. Set the injection path to be the `name` value, in this case being "TestData.txt"
4. On the next line, the system knows the injection path has been populated and attempts to do the following:
	1. Open the specified path -> `TestData.txt`
	2. Pull all lines of data from the txt and combine into one string with `\n` delimiter
	3. Parse the line using regular expressions to retrieve `public static String DATA = `
	4. Append `\" + fileContents \";` to the parsed string
	5. Set the current code line for writing to be the implemented string

This results in the following when converted to a single file:
```java
//AUTOGENERATED FROM ../src/TxtTestData.java

class TxtTestData {
    public static String DATA = "1\n2\n3\n4\n5\n6\n7\n8\n9\n10";
}
```

and everything works! In this case, because we are technically doing this at a "psuedo compile time" the `InjectData` is no longer used in the compressed Driver output.