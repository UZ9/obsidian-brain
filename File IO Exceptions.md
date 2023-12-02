##### File IO: Exceptions
- All IO-related exceptions are in `java.io

`FileNotFoundException` - File doesn't exist but is needed
- Thrown when `Scanner` cannot find file to scan from
- Thrown when `PrintWriter` cannot write to a file or file does not exist and can't create the file
`IOException` - More general IO problems
- `FileNotFoundException` extends `IOException`


Example: assume `winstreak.txt` doesn't exist

```java
File file = new File("winstreak.txt");
Scanner scan = new Scanner(file); // <-- THROWS FileNotFoundException HERE
int wins = scan.nextInt();

System.out.printf("We've won %d gmaes in a row!", wins);
```

To fix? 
- Write code inside try block, catch `FileNotFoundException`
- Delegate handling to another method, adding `throws FileNotFoundException`
