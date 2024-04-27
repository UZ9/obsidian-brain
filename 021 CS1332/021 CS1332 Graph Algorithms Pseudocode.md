[[023 CS1332 Final Exam]]


# Breadth-First-Search
```
bfs(start, graph):
	have map of adjacent vertices and their respective distances

	initialize set for visited vertcies
	initialize set for current queue, NOT priority queue
	initialize set for current vertices traversed

	add start to the queue

	while our queue is not empty:
		curr = dequeue the next node

		if curr is not in the visited set:
			add that vertex to the queue
			add that vertex to the visited set
```

# Depth-First-Search
- **Recursive-based search**

```
dfs(start, graph):
	have map of adjcanet vertices and their respective distances

	initialize set for visited vertices
	initialize set for vertices traversed

	call dfsHelper(adjacentList, start, visitedSet, traversalList)

	return traversal list

dfsHelper(curr, graph):
	add curr to visited vertices
	add curr to the traversed verticces

	for all adjacent vertices to curr:
		if that vertex is not in the visited list
			we call dfsHelper on that vertex

```


# Dijkstras

Runtime:

Dequeue: $O(\log e)$

If you do this $|E|$ times, the total runtime will be $O(|E| \log |E|)$. Some languages allow you to modify the priority within a priority queue, but *not* Java.

### Limitations

> [!danger] Negative Cycles
> - If total weight during a cycle is **negative**, a negative cycle occurs (Dijkstras fails)
> - Dijkstra will fail for any negative edge, **regardless** of whether the edge is negative or not

### Pseudocode
```
Dijkstras: (start: s): 
- create a set containing the vertices we already visited
- create a map <Vertex, Integer> of the distances create a priority queue of vertex distances (must have comparable) 
- have some sort of map of vertices adjacent to current vertex for all vertices

put them into the distance map with max integer value
add initial start with distance of 0, put into map with value 0

while the priority queue still has elements and we haven't reached the graph vertex size:
	u = remove next element from priority queue

	if we haven't visited u:
		add it to the visited list
		put it in the distance map 

		for all vertices adjacent to the vertex in question:
			if we haven't visited it, add it to the priority queue with u.dist + adjacent.dist

return visitedList
```