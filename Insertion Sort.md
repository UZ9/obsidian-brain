# Properties
- **Stable** - Yes
	- No non-adjacent swaps occur during insertion sort
- **Adaptive** - Yes
	- If the array is a fully sorted array, we only have to add each element to the sorted without any bubbling, resulting in $O(n)$ execution as opposed to its worse case scenario of $O(n^2)$.
- **In-place or out-of-place** - In-Place
	- No extra data structures used
# Big-O
- **Best Case** - $O(n)$
	- Array is already sorted
- **Average Case** - $O(n^2)$
	- Same as worst case
- **Worst case** - $O(n^2)$
	- Reverse sorted array (similar to [[Bubble Sort]]), where each element has to be bubbled over

# Overview (primarily from [[010 CS1331 MOC]])
##### Insertion Sort
Time Complexity: $O(n^2)$

Steps:
- **Insert** the first element of unsorted list by bubbling towards beginning until it is "relatively sorted"
- After each iteration, one more element has been relatively sorted
- After $k$ passes, the first $k + 1$ elements have been inserted into relatively sorted order

Optimization: If element to insert >= element on left, it is already in relatively sorted order

![[Pasted image 20231107105350.png]]
