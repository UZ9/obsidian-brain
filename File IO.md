I/O = input/output = reading, writing

Stream = flow of data (input/output are streams)

Files contain **data** we can read.

Files can be **written to**.

**Most IO classes are under `java.io`**

##### File Class
`import java.io.File`

- Abstract representation of a file, NOT the actual file

`new File("input.txt")` will create a File object
- Can use either relative path or absolute path

Most common methods:
- `exists()`, `isFile()`, `isDirectory()`, `canRead()`, `canWrite()`, `getAbsolutePath()`

##### File IO - Input
- Use a `Scanner` to read from a file, using the `file path`
- Uses `Scanner(File source)` constructor
	- Throws `FileNotFoundException` (CHECKED) exception if source cannot be found or path cannot be read

```java
import java.io.File;
import java.util.Scanner;

File file = new File("input.txt");
Scanner scan = new Scanner(file);

scan.nextInt();
```

##### File I/O - Output
- Use `PrintWriter` to write to files
- Uses methods `print()`, `printf()`, and `println()`
- Can either use `PrintWriter(File file)` or `PrintWriter(String fileName)`

> [!important] QUIRKS ABOUT PRINTWRITER
> - If a file with the file name **already exists**, the file will be **overwritten when the PrintWriter is created**
> - If the file **doesn't exist**, the PrintWriter will try to **create the file**
> - Throws **FileNotFoundException** (CHECKED) exception if file is not writable, or new file cannot be created

**IMPORTANT: BUFFERS**
When you write to a `PrintWriter` you aren't actually writing to the file! Instead, it's being stored in a **buffer** (think of an intermediate container) where it will **stay until you either flush() or close()** the `PrintWriter`. If you DON'T do these, nothing will be written!

`flush()` - pushes buffer into file, DOESN'T close the stream (you can continue to make edits)

`close()` - **flushes buffer**, closes stream, releases system resources
- Unable to write once closed
- ALWAYS close `PrintWriter` after finishing!


```java
import java.io.File;  
import java.io.FileNotFoundException; // <-- REMEMBER EXCEPTION IMPORTS!  
import java.io.PrintWriter;
	
public class Main {  
	// THROWS FILENOTFOUNDEXCEPTION
	public static void main(String[] args) throws FileNotFoundException {  
		PrintWriter writer = new PrintWriter(new File("output.txt"));  
		writer.println("Hello there!");  
		writer.close();  
	}  
}
```
