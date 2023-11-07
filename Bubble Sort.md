##### Bubble Sort
Time Complexity: $O(n^2)$

Steps:
- Iterate through list, **swap adjacent elements** that are unsorted
- As a result, the largest element is "bubbled" to the end of the unsorted list:
![[Pasted image 20231107104843.png]]

- After $k$ passes, the largest $k$ elements have been bubbled into final positions'

Potential Optimization: If no swaps are made, list is already sorted

![[Pasted image 20231107104942.png]]