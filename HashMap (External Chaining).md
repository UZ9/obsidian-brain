Relevant: [[HashMap]]
# Overview
- External chaining is a **closed addressing** strategy
- We store a [[LinkedList]] in each array index, where elements with duplicate hashcodes will be appended to either the front or end (will be specified during an exam)
- **no resizing** is needed for external chaining

##### Example
- All key values and their calculated compressed index:

![[Pasted image 20240424130130.png]]


- Put into the hashmap using external chaining:

![[Pasted image 20240424130143.png]]

# Big-O
- Reference [[HashMap#Big-O]]
# Operations
### Search
1. Calculate compressed index to search for
2. Iterate through the linked list at that compressed index to search
3. If we reach the end of the LinkedList and haven’t matched, element doesn’t exist in map
### Add
1. Calculate compressed index to search for
2. If there isn’t anything in that slot, create a new LinkedList with the new data entry as head
3. If there is a LinkedList already present, we either add to head to add to tail depending on implementation
### Remove
1. Calculate compressed index to search for
2. Traverse through the linked list at that compressed index to search
3. Once we’ve found the target element, we remove it (overall $O(n)$)