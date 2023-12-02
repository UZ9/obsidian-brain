Time complexity: $O(n*log(n))$

Best sorting algorithm covered in [[010 CS1331 MOC]], but almost entirely consists of [[Recursion]].

**Base case** - list of size 0 or 1 is already sorted
**Recursive calls** - split array into two halves, and merge sort each half
**Approaching base case** - repeatedly splitting list in half will eventually produce list of size 1

![[Pasted image 20231107161753.png]]

##### Big-O Comparison
![[Pasted image 20231107161809.png]]

![[Pasted image 20231107161818.png]]