### ArrayList
IMPORT:
```java
import java.util.ArrayList;
```

ArrayList = implements **List**
- List - **ordered** sequence of elements where duplicates **are** allowed

- Data is **stored in an array** behind the scenes
- Data is stored **contiguously in memory** (no null elements between non-null elements)

> [!important] On the topic of "contiguous in memory"
> The data values are stored side by side in memory, but in the case of a list of reference types (e.g. HotDog), this is **only the references** that are stored contiguously, NOT the actual values themselves

- Difference between `size` and `length/capacity`:
	- **size** - number of data **actually stored** in structure
	- **capacity** - maximum number of data that can be stored

ArrayList does **not** use brackets for indexing (like arrays), but instead methods.

##### Useful Methods & Diagrams
![[Pasted image 20231102163241.png]]

![[Pasted image 20231102163300.png]]


##### Initializing ArrayList
- You can technically declare an ArrayList with no type:

```java
ArrayList a = new ArrayList(); // stores Object types
```

Problems:
- Prone to casting errors (not type-safe)
- You would have to create a class for every type, e.g. `IntegerArrayList`, `StringArrayList` requiring code repetiton

Solution: **GENERICS!**