# Overview
- **LIFO** (last in first out) structure -> the newest element added to the stack is the first to go

![[Pasted image 20240420171103.png]]


# LinkedList Implementation
- To enqueue, add to front O(1)
- To dequeue (pop), remove from front O(1)
- No tail pointer needed
- SLL preferred over DLL as prev pointer isn't necessary
- To clear, set head to null

# Array Implementation
- To enqueue, add at index `size`
- To remove, set element at index `size` to null, decrement `size` (we want garage collection)
- To clear, reassign backing array to new empty array (**manually resetting would be O(n)**)

# Big-O


|                  | Top of stack | Push      | Pop  | Check Empty | Get Size | Clear | Resize     |
| ---------------- | ------------ | --------- | ---- | ----------- | -------- | ----- | ---------- |
| SinglyLinkedList | head         | O(1)      | O(1) | O(1)        | O(1)     | O(1)  | ***O(1)*** |
| Array Backed     | size - 1     | **O(1)*** | O(1) | O(1)        | O(1)     | O(1)  | O(n)       |
Notes:
> [!danger] Be careful about array backed pushing!
> The time complexity is $O(1)*$, NOT $O(1)$. 

