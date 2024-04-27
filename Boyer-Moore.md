# Overview
- Only uses the bad character rule
- When we encounter a bad character (mismatched character), we shfit by how many characters since the **last occurrence** in the table
- We build a **last occurrence table** to store the last index of each character in the form of a map


> [!danger] Boyer-Moore goes from **LEFT TO RIGHT**
> 
> This is different from all other pattern matching algorithms!

# Big-O
- Time complexity is same, regardless of whether you're using the Galil rule or not


### No Occurrences
- **Best Case** - $O(m + (n/m))$
	- We mismatch first character every time, text character is not in the pattern, allowing boyer moore to be used to full extent
	- Example
		- **Pattern** - bbbb
		- **Text** - aaaaaaaaaaaaaaaa
- **Worst Case** - $O(mn)$
	- We match every character until the end, where we mismatch; last occurrence is 1, 
	- Example
		- **Pattern** - baaa
		- **Text** - aaaaaaaaaaaaaaaaa
### Single Occurrence
- **Best Case** - $O(m)$
	- We match immediately; don't have to go any further
	- Example
		- **Pattern** - aaaa
		- **Text** - **aaaa**aaaaaaaaaaaaaaa
- **Worst Case** - $O(mn)$
	- Same as no occurrences, except we match at the very end: mismatch first character every time, but that character last index is 0 (no other of the same character), resulting in a shift of 1; same as brute force
	- Example
		- **Pattern** - baaa
		- **Text** - aaaaaaaaaaaaaa**baaa**

### All occurrences
- **Best Case** - $O(m + (n / m))$
	- We mismatch on the first character comparison (**RIGHTMOST** character, we go right to left), where that letter is the only letter at the end; allowing us to use boyer moore skips to their full extent
	- Example
		- **Pattern** - aaab
		- **Text** - aaacaaac**aaab**
- **Worst Case** - $O(mn)$
	- We match every character except for the starting character, where because it's at the start we would only shift by 1. Last match will only be at end of text, resulting in same performance as brute force
	- Example
		- **Pattern** - baaa
		- **Text** - aaaaaaaaaaaa**baaa**


