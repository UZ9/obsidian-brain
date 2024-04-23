# Overview
- Rather than storing data in an array like an [[ArrayList]], store the data in `Node` objects
- Each `Node` has a reference to the node in front of it, or back depending on type of LinkedList
- Data is **not** [[contiguous]]

![[Pasted image 20240420161107.png]]

![[Pasted image 20240420161128.png]]


# Tail vs No Tail
- Without tail pointer: adding to back, getting back, and remove back will be $O(n)$ regardless of the data structure (even with doubly linked list)
- With tail pointer: adding to back and getting back will be $O(1)$, removing from back will be $O(1)$ for DLL, otherwise $O(n)$ to reset tail
# Singly Linked List
- Each node only has a reference to the *next* element.
- Pros: less memory usage
- Cons: remove from back is $O(n)$ to update tail

## Doubly Linked List
- Each node has both a reference to the *next* element and *previous* element.
- Pros: remove from back is $O(n)$ **if it has a tail pointer**
- Cons: more memory usage

## Circular Singly/Doubly Linked List
- Same as SinglyLinkedList, but tail points to head
- Must use size as a termination condition, otherwise it would encounter an infinite loop

CLL can achieve addBack in O(1) without a tail pointer using the following trick:

```java
Node newNode = new Node(head.data);
newNode.next = head.next;
head.next = newNode;
head.data = data;
head = newNode;
```

![[IMG_0040.jpeg]]


# Big-O

| Operations            | SLL With Tail | SLL Without Tail | DLL With Tail | DLL Without Tail | CSLL (No Tail) |
| --------------------- | ------------- | ---------------- | ------------- | ---------------- | -------------- |
| addFront()            | O(1)          | O(1)             | O(1)          | O(1)             | O(1)           |
| addAtIndex()          | O(n)          | O(n)             | O(n)          | O(n)             | O(n)           |
| addBack()             | ***O(1)***    | O(n)             | O(1)          | O(n)             | O(1)           |
| removeFront()         | O(1)          | O(1)             | O(1)          | O(1)             | O(1)           |
| removeAtIndex()       | O(n)          | O(n)             | O(n)          | O(n)             | O(n)           |
| removeBack()          | O(n)          | **O(n)**         | ***O(1)***    | **O(n)**         | O(n)           |
| removeLastOccurence() | O(n)          | O(n)             | O(n)          | O(n)             | O(n)           |
| get()                 | O(n)          | O(n)             | O(n)          | O(n)             | O(n)           |
| getFront()            | O(1)          | O(1)             | O(1)          | O(1)             | O(1)           |
| getMiddle()           | O(n)          | O(n)             | O(n)          | O(n)             | O(n)           |
| getBack()             | ***O(1)***    | O(n)             | ***O(1)***    | O(1)             | O(n)           |
> [!info] Notable Confusions
> - Remove from back without a tail is still $O(n)$, as you must traverse to find the next node to be the tail (node right before). This time complexity is solved via a [[Doubly LinkedList]].
> - A doubly linked list has no advantage if it lacks a tail pointer


