# Overview
- Calculate MST of an undirected, connected graph


# Algorithm Ideas
1. Add every edge of graph into priority queue
2. While priority queue isn't empty **and** MST size not reached, we dequeue an edge from priority queue; if dequeued edge isn't a cycle, add to MST