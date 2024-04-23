# Overview 
- Prim's algorithm is a type of [[minimum spanning tree]]
- Prim's algorithm is a greedy algorithm--chooses the next lowest cost via a [[Heap (Priority Queue)]]-based queue
- If the graph is not connected, Prim's algorithm generates a **minimum spanning forest (MSF)**
- Focuses on buildnig an MST one vertex at a time by considering all existing edges
- *spanning tree* - tree connecting all vertices in a graph
- *minimum spanning tree* - spanning tree with smallest possible edge weight; minimum spanning trees are not unique


# Graph Cut
![[Pasted image 20240421215902.png]]

- Takes subset of vertices and all edges connecting them


# Algorithm Implementation
- Keep visited set for visited nodes
- [[Heap (Priority Queue)]] of **edges** with shortest distance being next edge
- Edges of minimum weight that are traversed are stored


# Big-O
- Same as Dijkstra's as it works almost identical to it: $O(|E| \log{|E|})$ 
	- If we were able to modify the priorities manually, we could have $O((|V| + |E|) \log {|V|})$
	- 