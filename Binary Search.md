TIME COMPLEXITY: $O(log(n))$
**REQUIRES ARRAY TO BE SORTED!!!**

- Much faster than linear search

Steps:
1. Find "middle element" of list. Compare middle element to target. If equal, element has been found. Otherwise:
2. Determine whether target element is on left or right side of middle element
	1. If target element < middle element, the target element must lie on the left half
	2. If target element > middle element, the target element must lie on the right half
3. Repeat steps 1 and 2 until:
	1. The element is found, OR
	2. There are no elements to compare with

![[Pasted image 20231102165026.png]]
