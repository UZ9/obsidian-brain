##### Selection Sort
Time Complexity: $O(n^2)$

Steps:
- **"Select"** smallest element in unsorted sublist, **swap** with beginning of unsorted list:
![[Pasted image 20231107105026.png]]

- After each iteration, next smallest element has been added to end of sorted list
- After $k$ passes, smallest $k$ elements have been swapped into their final positions
![[Pasted image 20231107105126.png]]