# Properties
- **Stable** - Yes
	- Duplicate elements are kept in order during Radix Sort
- **Adaptive** - No
	- The procedure will run the same amount of iterations regardless of whether the data is sorted or not
- **In-place or out-of-place** - out-of-place
	- Uses an array of `LinkedList` in order to sort the elements

# Big-O
- $k$ is the number of digits of the number with the largest magnitude
- $n$ is the number of elements
- For **all cases**, the time complexity will be $O(kn)$. 
# Overview
- Rather than sorting by comparing two numbers, we place numbers into **digit** buckets in order to sort them