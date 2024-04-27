# Overview
- Rather than [[HashMap (External Chaining)]]’s use of extra data structures, we **only use the original backing table**
- If we encounter a collision, we “probe” (shift index by a certain amount) to insert at a later index
- Consequently, the element might not be at its originally intended compressed index 
- When we delete elements, we do not set them to null, but instead create a **del marker**

# Linear Probing
- If we encounter collision, increment index by 1 and keep trying
- Calculated as $(H(k) + x) \% \text{table.length}$, where $x$ is the amount of times we’ve probed

# Quadratic Probing
- Instead of probing by going to the next direct element, we use the formula $(H(k) + x^2) \% \text{table.length}$, where $x$ is the current number of probes (0, 1, 4, 16, etc)

### Example
0: NULL  
1: <1, 1>  
2: <2, 13>  
3: <13, 2>  
4: NULL  
5: <11, 5>  
6: NULL  
7: NULL  
8: NULL  
9: NULL

- We're dealing with a size 10 hashmap, so our compression function  
  will be index % 10 
- We want to use quadratic probing, so our probing function is  
  (startingIndex + x^2) % 10, where x is the number of probes
- We want to insert <21, 1> into the hashmap

To start, calculate the starting index using the compression function:  
21 % 10 = 1 is our startingIndex

We check: is 1 currently occupied? Yes, so we have to probe. Our probing  
function is (startingIndex + x^2) % 10, and we now probe once, making it   
(1 + 1^2) % 10 = 2

We repeat these steps:

Is 2 occupied? Yes, so we probe again  
(1 + 2^2) % 10 = 5

Is 5 occupied? Yes, so we probe again   
(1 + 3^2) % 10 = 10 % 10 = 0

Is 0 occupied? Nope! We didn't have to deal with any DEL markers, so we   
go ahead and insert at this index.

# Operations

> [!important] When to stop probing
> We will **ALWAYS** stop probing once we’ve reached $size$ non-removed elements that we’ve probed 
 
### Search
1. Calculate compressed index, and check if this is what we want
2. If it happens to be the target key but is removed (del marker), we won’t find it
3. If it’s a 
4. Otherwise, we increment by the probing function and continue searching
### Add
1. Calculate compressed index, if it’s null we insert
2. If not null, we start probing
3. If it is a **del marker**, we mark the first del marker we’ve come across and continue
4. If we come across any value that is the key:
	1. If it is removed, we set it not to removed and set the data
	2. If it is not removed, we replace the value
5. If we get to a null spot, we check first if we’ve gotten a del marker; if we have, we use the del marker, otherwise use the null spot
### Remove
1. Calculate compressed index, then probe if needed
2. Once we’ve come across the element we need, we set it to removed
3. If we come across the element and it was already removed, we throw exception
### Resize
- We skip all del markers when resizing, create a new array, and rehash all existing keys