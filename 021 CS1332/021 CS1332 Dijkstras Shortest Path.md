# Overview
- Computes the shortest distance from one vertex to all other vertices in the graph
- Works specifically using **weighted graphs**o
- Works with both directed disconnected graphs
- Uses a [[Heap (Priority Queue)]]
- Assumes all weights are non-negative

[[Dijkstras Diagramming Example]]
# Algorithm Implementation
- Keep a visited set of visited nodes
- Keep a priority queue of vertices with their priority being the **cumulative distance**
- next vertex is the shortest path found
- shortest distances are stored in distance map


# Big-O
- Reality check was using old value, **don't trust it**
- The actual Big-O (confirmed by TA) is $O(|E| \log{|E|}$)
- [ ] find out why someone thought it was E + V