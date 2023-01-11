---
layout: post
title: "1443. Minimum Time to Collect All Apples in a Tree"
date: 2023-01-11 07:35:33 -0500
comments: true
---

Given an undirected tree consisting of n vertices numbered from 0 to n-1, which has some apples in their vertices. You spend 1 second to walk over one edge of the tree. Return the minimum time in seconds you have to spend to collect all apples in the tree, starting at vertex 0 and coming back to this vertex.

The edges of the undirected tree are given in the array edges, where edges[i] = [ai, bi] means that exists an edge connecting the vertices ai and bi. Additionally, there is a boolean array hasApple, where hasApple[i] = true means that vertex i has an apple; otherwise, it does not have any apple.

```javascript

/**
 * @param {number} _n
 * @param {number[][]} edges
 * @param {boolean[]} hasApple
 * @return {number}
 */

let n = 7,
  edges = [
    [0, 1],
    [0, 2],
    [1, 4],
    [1, 5],
    [2, 3],
    [2, 6],
  ];

let hasApple = [false, false, true, false, true, true, false];

var minTime = function (_n, edges, hasApple) {
  let n = _n;
  let graph = new Array(n).fill(0).map(() => new Array());
  for (let [u, v] of edges) {
    graph[u].push(v);
    graph[v].push(u);
  }
  let seen = new Array(n).fill(false);
  let ans = 0;
  const dfs = (u) => {
    seen[u] = true;
    let ret = false;
    for (let v of graph[u]) {
      if (seen[v]) continue;
      if (dfs(v)) {
        ans += 2;
        ret = true;
      }
    }
    return ret || hasApple[u];
  };
  dfs(0);
  return ans;
};
```

This one was confusing to me at first, this video (solving it with Python) helped me understand the problem better: [Minimum Time to Collect All Apples in a Tree - Leetcode 1443 - Python By NeetCodeIO](https://www.youtube.com/watch?v=Xdt5Z583auM)