Very similar system to [[021 CS1332 Depth First Search]]

# Overview
- Reach all connected vertices from a start vertex
- Uses a [[Queue]], Visited Set, and starting vertex
- Shortest path for unweighted graphs


## Algorithm
- Visit all vertices 1 edge away, then all two edges away, three edges...
- Prioritizes elements **closest** to start vertex
- Keep track of the visited vertices in a Set
- Initialize a queue for next vertices to process

> [!info] Handling ties when traversing
> For the most part, if two nodes are tied the next to be processed will be in **alphabetical order**.

```java
visitedSet = new Set<Vertex>();
queue = new Queue<Vertex>();

visitedSet.add(startVertex)
queue.add(startIndex)

while (queue has elements) {
	v = queue.remove();

	for (Vertex adj : adjacent nodes of v) {
		if (!visitedSet.contains(adj)) {
			visitedSet.add(adj);
			queue.add(adj);
		}
	}
}

```

# Big-O Efficiency
- Same as [[021 CS1332 Depth First Search]]: $O(|V| + |E|)$
	- We visit all vertices
	- We have to consider all edges

> [!danger] Trick question with graph density
> If it is stated that the graph is **sparse**, we know that $|E| \approx |V|$. As such, the time complexity would actually be $|V|$.
