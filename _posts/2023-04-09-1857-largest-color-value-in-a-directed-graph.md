---
layout: post
title: 1857. Largest Color Value in a Directed Graph
date: 2023-04-09 08:12 -0400
difficulty: hard
comments: true
---

There is a directed graph of `n` colored nodes and `m` edges. The nodes are numbered from `0` to `n - 1`.

You are given a string `colors` where `colors[i]` is a lowercase English letter representing the color of the ith node in this graph (0-indexed). You are also given a 2D array `edges` where `edges[j] = [aj, bj]` indicates that there is a directed edge from node `aj` to node `bj`.

A valid path in the graph is a sequence of nodes `x1 -> x2 -> x3 -> ... -> xk` such that there is a directed edge from `xi` to `xi+1` for every `1 <= i < k`. The color value of the path is the number of nodes that are colored the most frequently occurring color along that path.

Return the largest color value of any valid path in the given graph, or `-1` if the graph contains a cycle.

## Example

<img src="{{ site.baseurl }}/assets/images/apr-9.png" alt="Example grid image" />

```javascript
Input: colors = "abaca", edges = [[0,1],[0,2],[2,3],[3,4]]
Output: 3
Explanation: The path 0 -> 2 -> 3 -> 4 contains 3 nodes that are colored "a" (red in the above image).
```

## Solution

Good solution found [here](https://leetcode.com/problems/largest-color-value-in-a-directed-graph/solutions/3396557/js-dfs-solution/?orderBy=most_votes&languageTags=javascript).

```javascript
/**
 * @param {string} colors
 * @param {number[][]} edges
 * @return {number}
 */
var largestPathValue = function (colors, edges) {
  const n = colors.length;
  const visited = Array(n).fill(0);
  const maxCount = Array(n)
    .fill(0)
    .map((_) => Array(26).fill(0));
  const adj = Array(n)
    .fill(0)
    .map((_) => []);

  for (const [a, b] of edges) {
    // push b to a's adj list
    adj[a].push(b);
  }
  let res = 0;
  for (let i = 0; i < n; i++) {
    // dfs to find the max count of each color
    res = Math.max(res, dfs(i, maxCount));
  }
  return res === Infinity ? -1 : res;

  function dfs(node, colorsCount) {
    // if the node is visited, return the max count of the color
    const cur = colors[node].charCodeAt() - 97;
    if (!visited[node]) {
      visited[node] = 1;
      for (const next of adj[node]) {
        if (dfs(next, colorsCount) === Infinity) {
          return Infinity;
        }
        for (let k = 0; k < 26; k++) {
          // update the max count of each color
          maxCount[node][k] = Math.max(maxCount[node][k], maxCount[next][k]);
        }
      }
      maxCount[node][cur]++;
      visited[node] = 2;
    }
    // if the node is visited twice, return the max count of the color
    return visited[node] === 2 ? maxCount[node][cur] : Infinity;
  }
};
```
