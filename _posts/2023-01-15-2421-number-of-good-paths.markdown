---
layout: post
title: "2421. Number of Good Paths"
date: 2023-01-15 07:35:33 -0500
comments: true
difficulty: hard
---

There is a tree (i.e. a connected, undirected graph with no cycles) consisting of n nodes numbered from `0` to `n - 1` and exactly `n - 1` edges.

You are given a 0-indexed integer array `vals` of length `n` where `vals[i]` denotes the value of the `ith` node. You are also given a 2D integer array `edges` where `edges[i] = [ai, bi]` denotes that there exists an undirected edge connecting nodes `ai` and `bi`.

A good path is a simple path that satisfies the following conditions:

The starting node and the ending node have the same value.
All nodes between the starting node and the ending node have values less than or equal to the starting node (i.e. the starting node's value should be the maximum value along the path).
Return the number of distinct good paths.

Note that a path and its reverse are counted as the same path. For example, `0 -> 1` is considered to be the same as `1 -> 0`. A single node is also considered as a valid path.

This was behind my ability, but I found a great write up with a solution [here](https://leetcode.com/problems/number-of-good-paths/solutions/3052905/javascript-union-find/?languageTags=javascript)

```javascript
/**
 * @param {number[]} vals
 * @param {number[][]} edges
 * @return {number}
 */
const numberOfGoodPaths = (vals, edges) => {
  edges.sort((a, b) => {
    a = Math.max(...a.map((i) => vals[i]));
    b = Math.max(...b.map((i) => vals[i]));
    return a - b;
  });
  const link = [...Array(vals.length).keys()];
  const rank = [...Array(vals.length).keys()].map(() => 1);
  const count = [...Array(vals.length).keys()].map((i) => [vals[i], 1]);
  const find = (a) => {
    while (a != link[a]) {
      link[a] = link[link[a]];
      a = link[a];
    }
    return a;
  };
  const union = (a, b) => {
    a = find(a);
    b = find(b);
    if (a == b) return;
    if (rank[a] < rank[b]) [a, b] = [b, a];
    rank[a] += rank[b];
    link[b] = a;
    const [a_max_val, a_count] = count[a];
    const [b_max_val, b_count] = count[b];
    if (a_max_val == b_max_val) {
      count[a] = [a_max_val, a_count + b_count];
    } else if (a_max_val > b_max_val) {
      count[a] = [a_max_val, a_count];
    } else {
      count[a] = [b_max_val, b_count];
    }
  };

  const getPathsFromJoining = (a, b) => {
    a = find(a);
    b = find(b);
    if (a == b) return 0;
    const [a_max_val, a_count] = count[a];
    const [b_max_val, b_count] = count[b];
    if (a_max_val == b_max_val) {
      return a_count * b_count;
    }
    return 0;
  };
  let ans = 0;
  for (let [a, b] of edges) {
    ans += getPathsFromJoining(a, b);
    union(a, b);
  }
  return ans + vals.length;
};
```
