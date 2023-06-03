---
layout: post
title: 2101. Detonate the Maximum Bombs
date: 2023-06-02 08:07 -0400
difficulty: medium
comments: true
---

You are given a list of bombs. The range of a bomb is defined as the area where its effect can be felt. This area is in the shape of a circle with the center as the location of the bomb.

The bombs are represented by a 0-indexed 2D integer array `bombs` where `bombs[i] = [xi, yi, ri]`. `xi` and `yi` denote the X-coordinate and Y-coordinate of the location of the `ith` bomb, whereas `ri` denotes the radius of its range.

You may choose to detonate a single bomb. When a bomb is detonated, it will detonate all bombs that lie in its range. These bombs will further detonate the bombs that lie in their ranges.

Given the list of `bombs`, return the maximum number of bombs that can be detonated if you are allowed to detonate only one bomb.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-2.png" alt="matrix image" width="300"/>

```javascript
Input: bombs = [[2,1,3],[6,1,4]]
Output: 2
Explanation:
The above figure shows the positions and ranges of the 2 bombs.
If we detonate the left bomb, the right bomb will not be affected.
But if we detonate the right bomb, both bombs will be detonated.
So the maximum bombs that can be detonated is max(1, 2) = 2.
```

## Solution

Great solution found [here](https://leetcode.com/problems/detonate-the-maximum-bombs/solutions/1638829/javascript-dfs-solution/)

```javascript
/**
 * @param {number[][]} bombs
 * @return {number}
 */
var maximumDetonation = function (bombs) {
  //If there is only one bomb, return 1
  if (bombs.length <= 1) return bombs.length;

  //Declare the adjacency matrix
  let adj = {},
    maxSize = 0;
  //If we're inside the range of a bomb, return the bomb info
  const checkIfInsideRange = (x, y, center_x, center_y, radius) => {
    return (x - center_x) ** 2 + (y - center_y) ** 2 <= radius ** 2;
  };
  //CREATE ADJACENCY MATRIX with recursive DFS
  for (let i = 0; i < bombs.length; i++) {
    for (let j = i + 1; j < bombs.length; j++) {
      //If there is no adjacency matrix, create one
      if (!adj[i]) adj[i] = [];
      if (!adj[j]) adj[j] = [];
      let bombOne = bombs[i];
      let bombTwo = bombs[j];
      //If the bomb is inside the range of another bomb, add it to the adjacency matrix
      let fir = checkIfInsideRange(
        bombOne[0],
        bombOne[1],
        bombTwo[0],
        bombTwo[1],
        bombOne[2]
      );
      if (fir) adj[i].push(j);
      let sec = checkIfInsideRange(
        bombOne[0],
        bombOne[1],
        bombTwo[0],
        bombTwo[1],
        bombTwo[2]
      );
      if (sec) adj[j].push(i);
    }
  }

  //DEPTH FIRST SEARCH TO FIND ALL BOMBS TRIGGERED BY NODE
  const dfs = (node, visited) => {
    let detonated = 1;
    visited[node] = true;
    let childs = adj[node] || [];
    for (let child of childs) {
      if (visited[child]) continue;
      detonated += dfs(child, visited);
    }
    maxSize = Math.max(maxSize, detonated);
    return detonated;
  };
  //Run DFS on all bombs
  for (let i = 0; i < bombs.length; i++) {
    dfs(i, {});
  }
  return maxSize;
};
```
