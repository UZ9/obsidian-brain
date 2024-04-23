# Sorting Properties
- *stability* - a sorting algorithm is stable if it keeps order of duplicates; unstable if not (usually by non-adjacent swaps)
- *adaptive* - sorting algorithm can take advantage of how sorted the array was before sorting
	- usually in the form of extra optimizations, e.g. bubble sort quitting if data is already sorted
	- a not adaptive sorting algorithm will do the same thing regardless
- *in-place or out-of-place* - sorting algorithm is in-place if it doesn't use any extra data structures to sort, e.g. bubble sort; out-of-place if it uses an extra data structure, e.g. radix sort using extra buckets or merge sort creating subarrays
	- in-place will require more swapping in general
# Iterative Sort Overview
Sorts that iterate through a collection of data to sort unsorted pairs

Examples:
- [[Bubble Sort]]
- [[Insertion Sort]]
- [[Selection Sort]]
- [[Cocktail Shaker Sort]]