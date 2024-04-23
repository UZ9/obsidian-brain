# Graph Overview
- *graph* - non-linear structure of vertices connected by edges/arcs, defined as $G$
- *vertices* - points on graph with data associated
- *edges* - what connects vertices
- $G = (V, E)$ where
	- $E$ = edge set
		- For **directed** (digraph) graphs, pairs are $(u, v)$
			- $u$ = origination vertex
			- $v$ = destination vertex
		- For **undirected** graphs, pairs are $\{ u, v \}$
			- $u$ = first vertex
			- $v$ = second vertex
	- $V$ - vertex set
	- $|V|$ - order of graph
		- number of vertices within graph
		- seen sometimes as $n$
	- $|E|$ - size of graph
		- number of edges within graph
		- seen sometimes as $m$
		- a **tree** will always have $|V| - 1$ edges
			- likewise, if it has $|V| - 1$ edges it must be a tree 
	- $deg(v)$ - number of edges connected to vertex $v$
		- a vertex with no connections is deg 0, "isolated vertex"
- *directed vs undirected* - graph is directed if an edge points in a direction, if it points both ways it is undirected
- *incident* - if an edge is connected to a vertex, it is incident to that vertex
- *path* - set of edges connecting a pair of vertices
- *simple path vs walk vs trail*:
	- *simple path* - no repeated vertices, no repeated edges
	- *trail* - repeated vertices allowed, no repeated edges
		- *circuit* - trail where first and last vertices are connected (adjacent)
	- *walk* - repeated vertices allowed, repeated edges allowed

- *length of path* - number of edges traversed

### Example

![[Pasted image 20240421150143.png]]

> [!warning] Don't mix up order and size of graph!
> 
> The size of a graph is the **number of vertices**.
> 
> The order of a graph is the **number of edges**.
> 

- Order of graph ($|V|$) = 5
- Size of graph ($|E|$) = 6
- Degree of E = 2, connected to C and D


### Directed vs Undirected
![[Pasted image 20240421150905.png]]

- **all** edges must be directed within a directed graphs
- undirected edges have **no arrows**
- Length of path from A to C = multiple options; could be A -> B -> D -> C OR A -> C



### Weights
- graphs can be *weighted* or *unweighted*

![[Pasted image 20240421151327.png]]

- *weight* - how much does it cost to navigate this pathway (think of toll roads)


### Graph Types
- *dense graph* - graph is close to maximum number of edges

![[Pasted image 20240421151453.png]]


- *sparse graph* - close to minimum number of edges required to connect vertices
![[Pasted image 20240421151458.png]]

- *connected graph* - any node can get to any other node in the graph
![[Pasted image 20240421153128.png]]
- *strongly-connected graph* - connected AND every pair of vertices has a path between them
![[Pasted image 20240421153159.png]]
- *weakly-connected graph* - connected BUT not all vertices have a path between them 
![[Pasted image 20240421153242.png]]

- *disconnected graph* - at least two nodes where there is no way to get between them

![[Pasted image 20240421151654.png]]
- *simple graph* - no self-loop, no parallel edges
- *complex graph* (multigraph) - contains at least one self-loop or parallel edge

- *self-loop* - edge with same origin and destination
![[Pasted image 20240421151747.png]]
- *parallel edges* - two edges connecting same vertices, same orientation 
![[Pasted image 20240421151921.png]]

- *cycle* - vertices repeated in a path, first and last vertices adjacent
	- **must** be connected
![[Pasted image 20240421152218.png]]

- *acyclic graph* - no cycles, also known as a **tree**
	- **must** be connected
![[Pasted image 20240421152234.png]]


## Graph Representations
### Adjacency Matrix
- **Space Complexity** - $O(|V|^2)$ (number of vertices squared)
- best used when having a very **dense graph**
- **very bad** for inserting new vertices, as it requires creating a new matrix
- $V$ x $V$ array, where (row, column) is an edge from row to column
![[Pasted image 20240421153830.png]]
- e.g. edge from $A$ to $B$ has a weight of $e$
- for undirected graphs it will always be a *symmetrical matrix*

### Adjacency List
- **Space Complexity** - $O(|V| + |E|)$
- best used when having a **sparse graph**
- Store a map of each vertex to its incident edges
- Isolated vertices would have an empty list

![[Pasted image 20240421154415.png]]

### Edge List
- **Space Complexity** - $O(E)$
- best used when we need to only access edges
- not good for when there are disconnected nodes in graph
- store only connections between vertices
- isolated vertices not represented

![[Pasted image 20240421154540.png]]


# Graph Algorithms
[[021 CS1332 Depth First Search]]
[[021 CS1332 Breadth First Search]]
[[021 CS1332 Dijkstras Shortest Path]]
[[021 CS1332 Prims Algorithm]]
[[021 CS1332 Kruskals MST]]