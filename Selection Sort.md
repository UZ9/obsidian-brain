# Properties
- **Stable** - No
	- Because we're going through and picking a maximum or minimum and then swapping, we aren't swapping adjacent elements (making it an unstable algorithm)
- **Adaptive** - Yes
	- ddd
- **In-Place or Out-Of-Place** - In-Place
	- We don't use any extra data structures, so bubble sort would be out-of-place

> [!info] Why use selection sort?
> 
> It might seem at first glance that selection sort is completely useless compared to all of the other sorting algorithms. For the most part, you're correct! The only benefit of using selection sort over the other algorithms is 
# Big-O
- Because selection sort is **not adaptive**, the Big-O of selection sort will **ALWAYS** be $O(n^2)$.
# Overview (primarily from [[010 CS1331 MOC]])
- We keep track of a maximum (or minimum depending on situation) of the unsorted, where we then swap it with the first unsorted element after the sorted array.

Steps:
- **"Select"** smallest element in unsorted sublist, **swap** with beginning of unsorted list:
![[Pasted image 20231107105026.png]]

- After each iteration, next smallest element has been added to end of sorted list
- After $k$ passes, smallest $k$ elements have been swapped into their final positions

![[Pasted image 20231107105126.png]]