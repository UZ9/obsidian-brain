# Announcements:
- Homework 1 (ArrayLists): Due January 18th
- Homework 2: Due Thursday January 25 @11:55pm
- You're okay to save your work on GitHub, just make sure your repository is private

Extra Credit Opportunity: Visit the TAs at Office Hours before exam 1, get 1 extra point added to your score

Worksheets: Go to the **Recitation Worksheets**



ArrayList
- implementation of List ADT
- zero-aligned, contiguous
- **Always** starts at 0th index and no gaps
- Nice wrapper to more easily perform operatiopns on an array
- Technical details are hidden - abstraction


ArrayList Operations:
- adding: elements in and to right are right-shifted by 1
- removing: elements to right must be left-shifted by 1
- fixed capacity at assignment: if larger array becomes full, new larger array must be created and elements must be copied
- inefficient to copy elements over and insert and shift
	- instead, copy elements over to the LEFT (you could get a **deduction** if you don't do this)
- Must keep track of size variable, allowing adding to and removing from back in O(1) time

ArrayList speeds:

|  | Front | Middle | Back |
| ---- | ---- | ---- | ---- |
| Adding | O(n) | O(n) | O(1)* |
| Removing | O(n) | O(n) | O(1) |
| Accessing | O(1) | O(1) | O(1) |
Singly Linked List
- reference to the head (first node) and tail (last node)
- tail: back is O(1)
- - unable to remove from back because we have to modify pointer to the tail
- **not contiguous**
	- iterate through using while loop


|  |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- |
| With Tail | Adding | O(1) | O(n) | O(1) |
|  | Removing | O(1) | O(n) | O(n) |
|  | Accessing | O(1) | O(n) | O(1) |
| Without Tail |  | O(1) | O(n) | O(n) |
|  |  | O(1) | O(n) | O(n) |
|  |  | O(1) | O(n) | O(n) |

### Double Linked List
- nodes have a **prev** pointer, making modifying the list slihgtly trickier
- draw out the operations (easy to accidentally lose it)
- ALWAYS has a tail pointer to take advantage of preivous pointers--Java's LinkedList is a doubly linked list

- **when iterating to indices, start from closest end using size** - for full homework credit in efficiency
	- check if it's either > 1/2 size or < 1/2 size
	- 