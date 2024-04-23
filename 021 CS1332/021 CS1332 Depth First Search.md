Very similar system to [[021 CS1332 Breadth First Search]]
# Overview
- traversal algorithm that visits all reachable connections from a start, exploring as far down as it can before it explores elsewhere
- good for recursion and stacks

### DFS Recursive Steps
- at the start index, we DFS(start index) 
- for each DFS recursive:
	- add current to the visited list
	- we dfs all adjacent nodes not in visited list

# Big-O
- For DFS, we have to do 2 things:
	- Visit every vertex: $V$
	- Check every edge: $E$
- Efficiency: $O(|V| + |E|)$

# Applications
- Check if graph is connected
- Cycle detection
- spanning tree (all vertices connected with smallest number of edges)
- 
