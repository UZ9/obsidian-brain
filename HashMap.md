# Overview
- type of map:
	- stores data with a (**key, value**) system
	- keys are **unique**; if we put a value with the same key we replace the value
	- values are **not unique**
	- all maps are **searchable**
	- no order when used in a hash context
	- keys are **immutable**, values are not
- Uses an **array** as the backing table

# Big-O
(ripped from my piazza response)

Add, remove, and search all roughly use the same algorithm of first starting at the hashed index and then either probing if it's linear/quadratic probing, or traversing through the backing data structure if external chaining.

For **external chaining**, our **best and average** are 𝑂(1) for adding, removing, and searching, as on average assuming we have a good hash function will we expect a minimal amount of collisions when inserting into the map. However, our worst case gets a tad more complicated when it comes to choosing which data structure:

- We have to search for an element through the data structure regardless
- For **LinkedList**, worst case is we traverse through the entire structure: 𝑂(𝑛)
- For **ArrayList**, worst case is we traverse through the entire structure: 𝑂(𝑛)
- For **BST**, our worst case would be a generate tree, resulting in the same efficiency as a LinkedList of 𝑂(𝑛)
- For **AVL**, we remove our degenerate worst case from BST, making the operation instead 𝑂(log⁡𝑛)

For **linear and quadratic probing** (time complexity is same for the two), we now have to additionally consider resizing the array when we surpass the load factor. Our best and average cases for adding, removing, and searching will **still be 𝑂(1)**, however now the worst cases differ:

- For all three, the **worst case of probing** is probing 𝑂(𝑛) times (usually because of a bad hash function). As this is the only thing you really have to worry about with removing and searching, this results in a time complexity of 𝑂(𝑛) for removing and searching.
- When adding, our worst case would be **both probing and resizing**. As we might have to probe when creating a new resized backing table a bad hash algorithm can result in an add complexity of 𝑂(𝑛2).
# Operations
### put(Key, Value)
- if the key **does not exist**, we create a new entry with the (key, value)
- if the key **does exist**, we go ahead and replace the value, but keep the key

### remove(Key)
- find key, remove it (specific implementation depends on collision strategy shown below)
# How to insert into an array?
- We convert a key into its **hashcode** representation (an integer):
	- “Some Key” → 32839 in hashcode
	- “Another key” → 28383 in hashcode
- We then use a **compression function** to map the hashcode onto our backing array
	- this is usally $H(k)$ \% table.length, where $H(k)$ is the hashcode of the key and we mod it by the backing table’s length


# Dealing with collisions
- Collisions can be handled one of two ways: by **probing** to next empty slots, or **external chaining** by using additional data structures to handle multiple pieces of data mapping to the same index
- We keep a **maximum load factor** of when our backing table should resize as we keep adding elements; if we **exceed** the maximum balance factor, we resize to $2 * \text{currCapacity} + 1$
	- *load factor* - calculated as $\text{size} / \text{capacity}$, where size is the amount of non-null elements
		- maximum load factor is typically 60-70%
- Another strategy to avoid collisions is to use **prime numbers when possible** for the hashmap size

> [!danger] HashMaps rely on you having a good hashcode function!
> If we have a **bad hashcode**, it means we likely have several similar keys mapping to the same hashcode. As our goal is to avoid collisions, this is obviously unideal–as we see below the time complexity gets significantly worse as a result of constant collisions.

- If we choose to handle collisions by probing over to other indices in the array, we are dealing with **open addresssing** (we’re *open* to explore other indices). If we can only stick with the initial index resulting from our hashcode and use a data structure instead (i.e. external chaining), we are dealing with **closed addressing**.

![[HashMap (Probing) )]]


![[HashMap (External Chaining)]]