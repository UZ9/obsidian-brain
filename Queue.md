# Overview
- First in first out = oldest element is first to go (think of line)

![[Pasted image 20240420172702.png]]

# LinkedList Implementation
- Keep a head and tail
- To enqueue, add to back of linked list
- To dequeue, remove from front of linked list
- If doubly linked list, enqueueing and dequeuing can be done from either side 
## Array Implementation
- Requires a **circular array** implementation

![[Pasted image 20240420173013.png]]

- Front is start of data, back is next empty slot
- **All indices are modded by the array's length**
- For enqueue: set back to new data, back = (back + 1) % arr.length
- For dequeue: store front element to return, set front value to null, front = front + 1) % arr.length 
- If we reach the max capacity, we resize to 2x the size, then move all of the elements starting at 0, formula:

```java
void resize() {
	int[] newArr = new int[size * 2];

	for (int i = 0; i < size; i++) {
		newArr[i] = arr[(front + i) % table.length];
	}

	arr = newArr;
}
```