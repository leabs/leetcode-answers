---
layout: post
title: 2359. Find Closest Node to Given Two Nodes
date: 2023-01-25 07:34 -0500
difficulty: medium
comments: true
---

You are given a directed graph of `n` nodes numbered from `0` to `n - 1`, where each node has **at most one** outgoing edge.

The graph is represented with a given **0-indexed** array `edges` of size `n`, indicating that there is a directed edge from node `i` to node `edges[i]`. If there is no outgoing edge from `i`, then `edges[i] == -1`.

You are also given two integers `node1` and `node2`.

Return the **index** of the node that can be reached from both `node1` and `node2`, such that the maximum between the distance from `node1` to that node, and from `node2` to that node is minimized. If there are multiple answers, return the node with the **smallest** index, and if no possible answer exists, return `-1`.

Note that `edges` may contain cycles.

<pre><strong>Input:</strong> edges = [2,2,3,-1], node1 = 0, node2 = 1
<strong>Output:</strong> 2
<strong>Explanation:</strong> The distance from node 0 to node 2 is 1, and the distance from node 1 to node 2 is 1.
The maximum of those two distances is 1. It can be proven that we cannot get a node with a smaller maximum distance than 1, so we return node 2.
</pre>

## Solution

```javascript
/**
 * @param {number[]} edges
 * @param {number} node1
 * @param {number} node2
 * @return {number}
 */
function closestMeetingNode(edges, node1, node2) {
  //Declare maps to store the distance from each node to the other and count to count
  let map1 = {};
  let map2 = {};
  let count = 0;

  //Loop through the edges array and store the distance from each node to the other
  while (map1[node1] == undefined && node1 != -1) {
    map1[node1] = count;
    count++;
    node1 = edges[node1];
  }
  count = 0;
  //Loop through the edges array and store the distance from each node to the other
  while (map2[node2] == undefined && node2 != -1) {
    map2[node2] = count;
    count++;
    node2 = edges[node2];
  }
  //Declare a variable to store the max distance and a variable to store the result
  let max = Infinity;
  let res = -1;

  //Loop through the edges array and find the node that has the smallest max distance
  for (let i = 0; i < edges.length; i++) {
    //If the node is not in either map, continue
    if (map1[i] == undefined || map2[i] == undefined) continue;
    //Find the max distance between the two nodes
    let localMax = Math.max(map1[i], map2[i]);
    //If the max distance is smaller than the current max, update the max and the result
    if (localMax < max) {
      max = localMax;
      res = i;
    }
  }
  //Return the result
  return res;
}
```
