- **Overlapping** subproblems in recursion ("recursion on steroids")
	- *memoization* - Storing solutions to subproblems
- We have a recursive-based approach but implement it **iteratively** to avoid recursive costs
- *top-down DP* - implementing recursive solution and adding memoization
- *bottom-up DP* - computing solutions to subproblems in increasing order of complexity



# Fibonnaci Example
```python
fib(n):
	if n == 0 return 0
	if n == 1 return 1
	else 
		return fib(n - 1) + fib(n - 2)
```

Problems:
- Function is $O(2^n)$
- Same fib functions are repeatedly calculated:

![[Pasted image 20240423131056.png]]


## Solution
- Instead, store the results within an array:
- Recursive solution found first, then made iterative 

```python
fib(n):
	n[0] = 0
	n[1] = 1
	for i = 2 -> n:
		num[n] = num[n - 1] + num[n - 2]
	return num[n]
```

- $O(n)$ time complexity, $O(n)$ space complexity
# Examples


[[LCS]]