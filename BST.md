- BST is a type of [[binary tree]]
- Allows binary search to be performed, allowing $O(\log n)$ searches


> [!info] What about duplicate data?
> In [[023 CS1332 MOC]], duplicate data in trees will not be a handled case

# Shape Properties
- All properties of a [[binary tree]]
- Must follow: left child < node < right child

![[Pasted image 20240423222524.png]]

# Big-O
### `contains()` and  `add()`

| Best Case  | Average Case | Worst Case   |        |
| ---------- | ------------ | ------------ | ------ |
| contains() | $O(\log{n})$ | $O(\log{n})$ | $O(n)$ |
| add()      | $O(\log{n})$ | $O(\log{n})$ | $O(n)$ |
| remove()   | $O(\log n)$  | $O(\log n)$  | $O(n)$ |
- Worst case will always be a **degenerate tree**, something solved by instead using an [[AVL]]
- Another notable edge case is the best case of searching the node is $O(1)$ 
### Traversal

| Complexity |        |
| ---------- | ------ |
| PreOrder   | $O(n)$ |
| PostOrder  | $O(n)$ |
| InOrder    | $O(n)$ |
| LevelOrder | $O(n)$ |
- All traversals require going through all elements within the tree; no way to optimize this
# Traversals
### Preorder
- unique identifies a BST
- gives data closer to root faster

1. Process node data
2. Recurse left
3. Recurse right

```
preorder(Node node) {
	if node != null:
		process node data
		recurse left
		recurse right
}
```

### Inorder
- **not** unique, but gives data in **sorted** order


1. Recurse left
2. Process node data
3. Recurse right

```
inorder(Node node) {
	if node != null:
		recurse left
		process node data
		recurse right
}
```

### Postorder
- uniquely identifies a BST
- useful for removing leaf nodes

1. Recurse left
2. Recurse right
3. process data

```
postorder(Node node) {
	recurse left
	recurse right
	process data
}
```

### Levelorder
- uniquely identifies a BST
- breadth search

1. Create a queue and add root to the queue
2. While the queue is not empty:
	1. We dequeue the current node
	2. Process the current node
	3. Enqueue left child
	4. Enqueue right child


# Operations
### Search
- if we're less than the target, traverse left
- if we're greater than the target, traverse right
- if we're equal, return
- if we reach a null node, we didn't find it


### Add
- if we're less than the target, traverse left
- if we're greater than the target, traverse right
- if we're equal, we found a duplicate and shouldn't add
- if we reach null, the node doesn't exist yet and we add it


### Remove
- if we're less than the target, traverse left
- if we're greater than the target, traverse right
- if we're equal, we found item, remove it
- if we reach null, the node doesn't exist, throw exception

- once we've reached our target node:
	- if it's 0 children, we just remove
	- if it's 1 child, we connect child
	- if it's 2 children, we remove by either predecessor or successor

