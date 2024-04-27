# Overview
- Calculate MST of an undirected, connected graph
# Big-O
- Time Complexity: $|E| \log |E|$
	- Cycle detection is magic $O(1)$
- Data structure: $O(A^{-1}(n))$
	- $A(n)$ is [[Ackermann function]], grows really fast
	- Inverse of ackermann grows really slow: approximately $O(1)$


# Algorithm Ideas
1. Add every edge of graph into priority queue
2. While priority queue isn't empty **and** MST size not reached, we dequeue an edge from priority queue; if dequeued edge isn't a cycle, add to MST