---
layout: post
title: 1514. Path with Maximum Probability
date: 2023-06-28 09:14 -0400
difficulty: medium
comments: true
---

You are given an undirected weighted graph of `n` nodes (0-indexed), represented by an edge list where `edges[i] = [a, b]` is an undirected edge connecting the nodes `a` and `b` with a probability of success of traversing that edge `succProb[i]`.

Given two nodes `start` and `end`, find the path with the maximum probability of success to go from `start` to `end` and return its success probability.

If there is no path from `start` to `end`, return 0. Your answer will be accepted if it differs from the correct answer by at most 1e-5.

## Example

```javascript
Input: n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.2], start = 0, end = 2
Output: 0.25000
Explanation: There are two paths from start to end, one having a probability of success = 0.2 and the other has 0.5 * 0.5 = 0.25.
```

## Solution

Good solution [here](https://leetcode.com/problems/path-with-maximum-probability/solutions/1585282/javascript-solution-dijkstra-s-algorithm/)

```javascript
var maxProbability = function(n, edges, succProb, start, end) {
    const MIN = Number.MIN_SAFE_INTEGER;
    const m = edges.length;
	
    // Create an adjacency list to represent the graph
    const adjList = {};
    // Initialize an array to store the maximum probability of reaching each node
    const dists = new Array(n).fill(MIN);
    
    // Construct the adjacency list
    for (let i = 0; i < n; i++) {
        adjList[i] = [];
    }
    
    for (let i = 0; i < m; i++) {
        const [u, v] = edges[i];
        const weight = succProb[i];
        
        adjList[u].push([v, weight]);
        adjList[v].push([u, weight]);
    }
    
    // Create a max heap to store the maximum probability of reaching each node
    const maxHeap = new MaxPriorityQueue({ priority: x => x[1] });
    
    // Enqueue the start node with a probability of 1
    maxHeap.enqueue([ start, 1 ]);
    
    // While the heap is not empty
    while (!maxHeap.isEmpty()) {
        // Dequeue the node with the maximum probability of reaching it
        const [ node, prob ] = maxHeap.dequeue().element;
        
        // If we have reached the end node, return the probability
        if (node === end) return prob;
        
        // If we have already found a path with a greater probability, skip this node
        if (dists[node] > prob) continue;
        
        // Iterate through the neighbors of the current node
        for (const [nei, weight] of adjList[node]) {
            // If the probability of reaching the current neighbor is greater than the current maximum probability, update the maximum probability and enqueue the neighbor
            if (prob * weight > dists[nei]) {
                dists[nei] = prob * weight;
                maxHeap.enqueue([nei, dists[nei]]);
            }
        }
    }
    
    // If we have not found a path to the end node, return 0
    return 0;
};
```
