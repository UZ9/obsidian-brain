- AVLs are a type of [[BST]] with the worst case degenerative tree removed via balancing
	- Eliminates worst case $O(n)$, allowing all operations to be $O(\log n)$

# Big-O
- $O(\log n)$ for everything!
# Balance information
- Height and balance factor are stored in each node
### Height - $O(1)$
- Calculated as max(leftChildHeight, rightChildHeight) + 1
	- height of leaf is 0, height of null is -1
- Stored within each node
### Balance Factor - $O(1)$
- Calculated as height(left child) - height(right child) 
- Stored within each node

### Balanced vs Unbalanced
- A node is considered **balanced** if the balance factor's magnitude > 1 (i.e. < -1 || > 1)
	- Balanced if it's -1, 0, 1
- If the balance factor is > 1, it is **left heavy**
- If the balance factor is < 1, it is **right heavy**
# Rotations
- All rotations are $O(1)$
![[Pasted image 20240423231922.png]]

### Single Rotations

##### Left Rotation
![[Pasted image 20240423231818.png]]

##### Right Rotation
![[Pasted image 20240423231856.png]]

### Double Rotations
##### Right-Left Rotation
![[Pasted image 20240423232001.png]]


##### Left-Right Rotation
![[Pasted image 20240423232015.png]]



