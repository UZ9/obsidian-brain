# 1332 ArrayList
- Uses an array as the backing structure, **automatically resized when needed**
- *size* - number of data stored
- *capacity* - number stored without resize

## Properties
- **Must be** [[contiguous]] and zero-aligned
- Size is stored in a variable for efficient operations, we use it for next empty spot in O(1)

![[Pasted image 20240420160432.png]]

## Resize Case
- When the ArrayList size reaches capacity, we resize, typically to original capacity multiplied by two.
- We create a new array with the resized capacity and move all elements from the previous array over, resulting in $O(n)$ time complexity.
## Big-O
### Add to Front - O(n)
- Add to front requires shifting all elements over to keep contiguous property

### Add at index - O(n)
- Adding to an arbitrary index will require shifting all elements over to keep contiguous property



### Add to Back - $O(1)*$
- Because resizing is so rare for ArrayLists, saying that add to the back is $O(n)$ wouldn't be providing the entire picture. Instead, we use the [[amortized]] time complexity, or **cost over time**. Therefore adding to the back is $O(1)$ amortized, or $O(1)*$. 

> [!warning] Potential confusion on wording
> If the exam is asking for the **worst time complexity**, we ignore the amortized complexity. Adding to the back would be $O(n)$ due to the edge case.
>
>If the exam is asking for the **amortized** time complexity, the time complexity of adding to back is $O(1)$

### Remove from Front - O(n)
- Requires shifting all elements over to keep contiguous

## Remove at index - O(n)
- Requires shifting all elements over to keep contiguous

## Remove from back - O(1)
- No shifting required, we just set the last element index to null

## Remove last occurrence - O(n)
- Requires looping through the array to see what the last element is. We can optimize this by starting from the back of the array, but it will still be $O(n)$

## Get anything (front, middle, back, index) - O(1)
- ArrayList is index based, easy to access via array

# 1331 ArrayList
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