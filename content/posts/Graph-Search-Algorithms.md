---
title: 'Graph Search Algorithms'
date: 2022-12-15T15:23:19+08:00
draft: false
math: true
---

Revise about many graph-searching related algorithms.

## DFS: Depth First Search

Search till the leaf vertex then choose another path.

It will find a path between two vertices and it's _guaranteed_ to do so, however it is _not guaranteed_ to find the shortest path.

works on graphs that are:

- connected
- unweighted
- directed

Uses a stack data structure to traverse all nodes in a graph.

Steps of the algorithm:

1. push the root vertex to the stack
2. while the vertex is not empty
   1. pop a vertex out of the stack
   2. if the vertex is:
      1. the destination, then end search
      2. marked visited, then `continue`
      3. unvisited:
         1. mark it as visited
         2. add its unvisited neighbors to the stack

## BFS: Breadth First Search

Search all neighbors of a vertex then move on next level.

It is _guaranteed_ to find the shortest path.

works on graphs that are:

- connected
- unweighted
- directed
- cyclic

Uses a queue data structure to traverse all nodes in a graph.

Steps of the algorithm:

1. push the root vertex to the queue
2. mark the vertex visited
3. while the queue is not empty:
   1. pop a vertex from queue
   2. if the vertex is:
      1. the destination, then end search
      2. else:
         1. mark its unvisited neighbors as visited
         2. push said neighbors to the queue

## Uniform Cost Search

an _adaptation_ of breadth-first search to make it work on weighted graph

works on graphs that are:

- connected
- weighted: no negative edges
- directed
- cyclic

## Dijkstra Algorithm

This algorithm find the shortest path from a vertex to all other vertices

Using 2 data structures:

- a priority queue of vertices
- lists of:
  - shortest distance and
  - preceding vertices in shortest path

The steps of this algorithm are:

1. Set up auxiliary data structures
2. While the priority queue has unexplored vertices:
   1. Take the next vertex from the priority queue
   2. Follow its edges and update any distances

Its time complexity depends on the data structures used.

If we are using a heap for the priority queue and two array, the time complexity is $$O((V + E)logV)$$

This algorithm works on graphs that are:

- directed
- weighted: only guaranteed to be correct when there are no negative edges

## Floyd-Warshall Algorithm

```C
for (i = 1; i <= n; i++) {
    for (j = 1; j <= n; j++) {
        if (e[i][j] > e[i][1] + e[1][j]) {
            e[i][j] = e[i][1] + e[1][j];
        }
    }
}
```

For every intermediate vertex check if there is a shorter path from start to end point through the intermediate.
