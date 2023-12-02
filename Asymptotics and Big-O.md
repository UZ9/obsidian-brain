### Asymptotics/Big-O
Asymptotics - "growth rate of number of operations as input size grows"
- Measures **efficiency** of algorithm, NOT running time

Big-O - example of asymptotic notation
- **Upper bound** of growth rate (what is the **maximum** time this method could take?)
- Ignores non-dominating terms and constants
	- **Non-dominating**: insignificant as input size increases
	- **Multiplicative constants**: no impact on growth rate
- Example: $O(n^2)$ = as input size grows linearly, total operations grows by factor of $n^2$ 

##### Very useful diagram (potentially memorize)
![[Pasted image 20231102164503.png]]

##### Determining Big-O of code?
- Calculate amount of operations performed on each element in the input
##### Big-O Example
![[Pasted image 20231102164611.png]]
