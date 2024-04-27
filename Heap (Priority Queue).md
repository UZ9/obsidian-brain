# Overview
- All heaps are [[binary tree]]s, but not [[BST]]
- All heaps must be **complete** (filled left to right)
- Implemented via an array, where the array represents the [[level order]] traversal
- A **MaxHeap** is where the **largest item** is the root, while a **MinHeap** is where the **smallest item** is the root

> [!danger] **ALWAYS REMEMBER THAT HEAPS START AT 1**
> The first element in the array will be null.

Minheap Example:
![[Pasted image 20240423213029.png]]

### Finding Children
- For any node at index $n$:
	- Left child is $n * 2$
	- Right child is $n * 2 + 1$
	- Parent is $n / 2$
- index **size** will give the last element in the heap


# Properties
- Not designed for searching: $O(n)$
- Used as **priority queues**, as it's $O(1)$ to find highest priority


# Big-O
- **add** - $O(\log n)$*
	- adding element to end is $O(1)$, upheap is $O(\log n)$
	- worst case is having to resize, requiring $O(n)$
- **remove** - $O(\log n)$
	- removing head is $O(1)$, swapping with last element is $O(1)$, downheaping is $O(\log n)$
- **buildheap** - $O(n)$
	- ...for reasons outside of this class




# Operations

### BuildHeap - O($n$)
- Takes unsorted, unordered array and converts it into a heap
- Much better than the naive way of adding all elements (which would be $O(n \log n)$)

> [!info] Why is it $O(n)$?
> We don't have a formal proof for how it's $O(n)$, but we do know the following:
> - Down-Heap is an $O(\log n)$ operation
> - We need $n / 2$ Down-Heap operations
> - Most of the data on the bottom requires $O(1)$ operations, while the other half is around $O(\log n)$, eventually averaging out to $O(n)$


> [!important] BuildHeap should **ABSOLUTELY** be known for the final
> This was something mentioned by Faulkner as something that "either is on Exam 2 or the final" and it wasn't present on exam 2.

[[023 CS1332 BuildHeap Diagram Example]]
### Add - $O(\log n)$*
Steps:
1. Add element to next spot in array (index size)
2. **Upheap** starting from new data to fix

- Note: worst case is having to resize, which is $O(n)$
### Remove - $O(\log n)$
Steps:
1. Remove element from the root
2. Move the last element of the heap to replace the root
3. Downheap the new root

### Upheap - $O(\log n)$
- Start from bottom, keep going up while target node and swapping if out of order

### Downheap - $O(\log n)$
- Start from current node, keep going down while target node is not in correct order relationship
- If there are two children, we must compare data with the higher priority child, but this will require 2 comparisons (one between children, one between that node and the one above)