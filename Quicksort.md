# Properties
- **Stable** - No
	- Non-adjacent elements are swapped, where previous order of duplicate elements does not persist
- **Adaptive** - No
	- Quicksort will always do the same thing regardless of whether the data is sorted or not; can't detect if sorted or not
- **In-place or Out-of-place** - In-place
	- No extra data structures used for quicksort

> [!info] Confusion about "iteration"
> An iteration for Quicksort is a recursive call that is not a length 0 base case.
# Big-O
- **Best Case** - $O(n \log n)$
	- Pivot is **always** the median value of subarray
- **Average Case** - $O(n \log n)$
- **Worst Case** - $O(n^2)$
	- Pivot is always the min or max, value of subarray

# Algorithm Steps
