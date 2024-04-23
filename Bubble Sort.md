# Properties
- **Stable** - Yes
	- Only adjacent elements are swapped
- **Adaptive** - Yes
	- Example: array is already sorted, so we only require one pass of bubble sort
- **In-Place or Out-Of-Place** - In-Place
	- We don't use any extra data structures, so bubble sort would be out-of-place
# Big-O
- **Best Case** - $O(n)$
	- Data is already sorted, we only make one iteration through the loop
- **Average Case** - $O(n^2)$
	- Same as worst case
- **Worst Case** - $O(n^2)$
	- Worst case is a reversed sorted array, in which we have to bubble n times requiring $n^2$ passes



# Optimizations
- We can reduce the amount of swaps on average by only iterating to where the last swap was made, as everything after can be assumed to be sorted.

- Example diagram with optimization:
![[IMG_0041.jpeg]]
# Overview (mostly from [[010 CS1331 MOC]])
Bubble sort is an [[iterative sort]]

Steps:
- Iterate through list, **swap adjacent elements** that are unsorted
- As a result, the largest element is "bubbled" to the end of the unsorted list:
![[Pasted image 20231107104843.png]]

- After $k$ passes, the largest $k$ elements have been bubbled into final positions'

Potential Optimization: If no swaps are made, list is already sorted

![[Pasted image 20231107104942.png]]
