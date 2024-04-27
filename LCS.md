LCS is the primary example in [[023 CS1332 MOC]] of [[dynamic programming]]

# Overview
- LCS - longest common subsequence
- *sequence* - sequence of characters in same relative order, not necessarily [[contiguous]]
	- **all** substrings are subsequences, not all subsequences are substrings

# Brute force vs DP
- **Brute force** - we try to compare every single subsequence of one string to another string
	- Requires $2^n$ subsequences for each string, incredibly inefficient

- **Dynamic programming** - store length of LCS for substrings, keep adding characters
	- Left to right, then top to bottom
	- If the row and column character match, we increase the length

# Big-O
- Time complexity: $O(mn)$

# DP Algorithm
1. Create $n + 1$ by $m + 1$ array
	- $n$ is length of first string
	- $m$ is length of second string
2. Fill row 0 and column 0 with 0s
3. For each cell `L[i][j]` from i=1->n, j=1->m:
	1. if characters are equal, set value to 1 + (previous diagonal value)
	2. if characters are not equal:
		1. if above and left are the same, take from left
		2. else, set it to max of above value and left value

### Diagramming

> [!info] Tips for diagramming quickly
> - If the letter does **not exist** within the the other string, we **copy the numbers** of the previous row.