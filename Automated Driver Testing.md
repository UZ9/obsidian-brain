[[Main Driver]]

Written by Ryder Johnson, 11/3/23

### Introduction
CS1331 Homework assignments can be unforgiving. From what feels like hundreds of possible constructors to the many, *many* edge cases, thoroughly testing each component has exponentially increased with every week--with a need for a streamlined process.

When I initially got together with Justin for HW4, we identified the issues plaguing older iterations of our drivers, and came up with the following restrictions:
- **Portable** - Arguably the largest (and most painful) limitation: everything must be in a single `.java` file. The end user should be able to directly drag the file into their project with no other requirements, leading to the unfortunate complications of:
	- **No more than one file** - EVERYTHING must be contained in a single `.java` file for distribution.
	- **No outside dependencies** - No JUnit, Mockito, Selenium, etc. to use for easy test creation. As seen later on in this article, we essentially wrote our own variant of JUnit.
- **Robust Tests** - Tests must be easy to create, easy to read, and easy to modify if needed.
	- **Feedback-based System** - The tests should notify the developer of specifically *what* they missed, along with the stack trace of where it might have occurred. 
	- **Exception Handling** - All sorts of exceptions--some intentional--can be thrown from the end user's code. In order to prevent this from breaking the entire testing environment, these are caught and internally handled. 
	- **"No clutter nonsense"** - Tests should be as clear and intuitive to read as possible, requiring a few terminal tricks for formatting. 

### What does a test look like?
Before delving into the nitty gritty details of the project, take a look at an example of a test:
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
- `@InjectData` - Injects data from `.txt` and inserts it into a String. This ended up being a massive change and has a section here dedicated to the new system works.