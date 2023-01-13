---
layout: post
title: "1519. Number of Nodes in the Sub-Tree With the Same Label"
date: 2023-01-12 07:35:33 -0500
comments: true
difficulty: medium
---

You are given a tree (i.e. a connected, undirected graph that has no cycles) consisting of n nodes numbered from 0 to n - 1 and exactly n - 1 edges. The root of the tree is the node 0, and each node of the tree has a label which is a lower-case character given in the string labels (i.e. The node with the number i has the label labels[i]).

The edges array is given on the form edges[i] = [ai, bi], which means there is an edge between nodes ai and bi in the tree.

Return an array of size n where ans[i] is the number of nodes in the subtree of the ith node which have the same label as node i.

A subtree of a tree T is the tree consisting of a node in T and all of its descendant nodes.

```javascript
/**
 * @param {number} n
 * @param {number[][]} edges
 * @param {string} labels
 * @return {number[]}
 */
var countSubTrees = function (n, edges, labels) {
  // build graph
  const graph = new Map();
  // init graph
  for (let i = 0; i < n; i++) {
    graph.set(i, []);
  }
  // add edges
  for (let [a, b] of edges) {
    graph.get(a).push(b);
    graph.get(b).push(a);
  }
  const ans = new Array(n).fill(0);
  const seen = new Set();
  const dfs = (node) => {
    const count = new Array(26).fill(0);
    seen.add(node);
    for (let nei of graph.get(node)) {
      if (!seen.has(nei)) {
        const sub = dfs(nei);
        for (let i = 0; i < 26; i++) {
          count[i] += sub[i];
        }
      }
    }
    count[labels.charCodeAt(node) - 97]++;
    ans[node] = count[labels.charCodeAt(node) - 97];
    return count;
  };
  dfs(0);
  return ans;
};
```
