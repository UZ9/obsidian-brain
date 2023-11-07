##### Insertion Sort
Time Complexity: $O(n^2)$

Steps:
- **Insert** the first element of unsorted list by bubbling towards beginning until it is "relatively sorted"
- After each iteration, one more element has been relatively sorted
- After $k$ passes, the first $k + 1$ elements have been inserted into relatively sorted order

Optimization: If element to insert >= element on left, it is already in relatively sorted order

![[Pasted image 20231107105350.png]]
