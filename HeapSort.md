# Overview
- HeapSort is a very straightforward sort as it's only using a [[Heap (Priority Queue)]]'s `BuildHeap` to automatically sort elements (minheap), and then dequeuing after

# Properties
- **Stable** - No
	- BuildHeap and remove operations aren't keeping duplicate elements in same order, resulting in unstable sort 
- **Adaptive** - No
	- Sort does the same operations every time regardless of whether it's sorted or not
- **In-place or Out-of-place** - Out of place
	- Sort has to use an external data structure (heap)

# Big-O
- Big-O is $O(n \log n)$ for **all** cases (best, average, and worst are all the same)
- BuildHeap is $O(n)$, and removing an element from a heap is $O(\log n)$
- We have to remove all $n$ elements from the heap, resulting in a removal time of $O(n \log n)$
- $O(n) + O(n \log n) = O(n \log n)$, resulting in our final time complexity of $O(n \log n)$.

# Algorithm Steps
1. Add all elements to a heap
2. Dequeue the elements of the heap. These in order will be the sorted elements
3. Return the dequeued elements in order