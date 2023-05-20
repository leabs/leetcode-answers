---
layout: post
title: 785. Is Graph Bipartite?
date: 2023-05-19 09:18 -0400
difficulty: medium
comments: true
---

There is an **undirected** graph with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array `graph`, where `graph[u]` is an array of nodes that node u is adjacent to. More formally, for each v in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:

- There are no self-edges (`graph[u]` does not contain `u`).
- There are no parallel edges (`graph[u]` does not contain duplicate values).
- If `v` is in `graph[u]`, then `u` is in `graph[v]` (the graph is undirected).
- The graph may not be connected, meaning there may be two nodes `u` and `v` such that there is no path between them.

A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that every edge in the graph connects a node in set `A` and a node in set `B`.

Return `true` if and only if it is bipartite.

## Example

<img src="{{ site.baseurl }}/assets/images/may-19.jpg" alt="Example tree image"  style="max-width:300px" />

```javascript
Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
Output: false
Explanation: There is no way to partition the nodes into two independent sets such that every edge connects a node in one and a node in the other.
```

## Solution

Good solution found [here](https://leetcode.com/problems/is-graph-bipartite/solutions/1991317/javascript-solution-using-bfs/)

```javascript
/**
 * @param {number[][]} graph
 * @return {boolean}
 */
var isBipartite = function (graph) {
  //Set up a color array
  let colorArr = new Array(graph.length).fill(-1);
  colorArr[0] = 1;
  let queue = [];
  //FOR the length of the graph
  for (let i = 0; i < graph.length; i++) {
    //IF the graph at i has a length
    if (graph[i].length > 0) {
      //Push i to the queue
      queue.push(i);
    }
  }
  //WHILE the queue has a length
  while (queue.length) {
    let top = queue.shift();
    let neighbors = graph[top];
    //FOR the length of the neighbors
    for (let node of neighbors) {
      //IF the colorArr at node is -1
      if (colorArr[node] === -1) {
        //Set the colorArr at node to 1 - colorArr at top
        colorArr[node] = 1 - colorArr[top];
        //Push node to the queue
        queue.push(node);
      }
      //ELSE IF the colorArr at node is equal to the colorArr at top
      else if (colorArr[node] === colorArr[top]) {
        return false;
      }
    }
  }
  return true;
};
```
