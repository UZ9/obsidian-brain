# Properties
- **Stable** - Yes*
	- IMPORTANT: when merging and two numbers are the same, it **must** take from the left subarray!
- **Adaptive** - No
	- Runs the same steps regardless of whether it's sorted or not
- **In-place or Out-of-place** - Out-of-place 
	- The algorithm have multiple subarrays that it uses to sort the data,  using extra memory

# Big-O
- **Best Case** - $O(n \log{n})$
	- Not adaptive; will always do the same thing regardless (log n splits, log n merges, n visits per split/merge)
- **Average Case** - $O(n \log n)$
	- Not adaptive
- **Worst Case** - $O(n \log n)$
	- Not adaptive

# Overview (primarily from [[010 CS1331 MOC]])
Time complexity: $O(n*log(n))$

Best sorting algorithm covered in [[010 CS1331 MOC]], but almost entirely consists of [[recursion]].

**Base case** - list of size 0 or 1 is already sorted
**Recursive calls** - split array into two halves, and merge sort each half
**Approaching base case** - repeatedly splitting list in half will eventually produce list of size 1

![[Pasted image 20231107161753.png]]

##### Big-O Comparison
![[Pasted image 20231107161809.png]]

![[Pasted image 20231107161818.png]]