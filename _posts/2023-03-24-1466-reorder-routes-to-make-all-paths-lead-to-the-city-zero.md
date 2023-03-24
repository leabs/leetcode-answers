---
layout: post
title: 1466. Reorder Routes to Make All Paths Lead to the City Zero
date: 2023-03-24 10:37 -0400
difficulty: medium
comments: true
---

There are `n` cities numbered from `0` to `n - 1` and `n - 1` roads such that there is only one way to travel between two different cities (this network form a tree). Last year, The ministry of transport decided to orient the roads in one direction because they are too narrow.

Roads are represented by `connections` where `connections[i] = [ai, bi]` represents a road from city `ai` to city `bi`.

This year, there will be a big event in the capital (city `0`), and many people want to travel to this city.

Your task consists of reorienting some roads such that each city can visit the city `0`. Return the **minimum** number of edges changed.

It's **guaranteed** that each city can reach city `0` after reorder.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-24.png" alt="Example tree image" />

```javascript
Input: n = 6, connections = [[0,1],[1,3],[2,3],[4,0],[4,5]]
Output: 3
Explanation: Change the direction of edges show in red such that each node can reach the node 0 (capital).
```

## Solution

```javascript
/**
 * @param {number} n
 * @param {number[][]} connections
 * @return {number}
 */
var minReorder = function (n, connections) {
  //reorienting some roads such that each city can visit the city `0`. Return the **minimum** number of edges changed.
  //create a graph
  const graph = new Array(n).fill().map(() => []);
  //add the connections to the graph
  for (const [v1, v2] of connections) {
    //add the connection to the graph
    graph[v1].push(v2);
    //add the connection to the graph
    graph[v2].push(-v1);
  }
  //start at node 0
  const queue = [0];
  //add node 0 to the visited set
  const visited = new Set([0]);
  let ans = 0;
  //while the queue is not empty
  while (queue.length > 0) {
    //get the current node
    const node = queue.shift();
    //loop through the neighbors
    for (const neighbor of graph[node]) {
      //if the neighbor is not visited
      if (!visited.has(Math.abs(neighbor))) {
        //add the neighbor to the visited set
        visited.add(Math.abs(neighbor));
        //if the neighbor is positive, increment the answer
        if (neighbor > 0) ans++;
        //add the neighbor to the queue
        queue.push(Math.abs(neighbor));
      }
    }
  }
  return ans;
};
```
