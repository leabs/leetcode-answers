---
layout: post
title: 1162. As Far from Land as Possible
date: 2023-02-10 08:09 -0500
difficulty: medium
comments: true
---

Given an `n x n` `grid` containing only values `0` and `1`, where `0` represents water and `1` represents land, find a water cell such that its distance to the nearest land cell is maximized, and return the distance. If no land or water exists in the grid, return `-1`.

The distance used in this problem is the Manhattan distance: the distance between two cells `(x0, y0)` and `(x1, y1)` is `|x0 - x1| + |y0 - y1|`.

## Example

<pre>
    <strong>Input:</strong> grid = [[1,0,1],[0,0,0],[1,0,1]]
    <strong>Output:</strong> 2
    <strong>Explanation:</strong> The cell (1, 1) is as far as possible from all the land with distance 2.
</pre>

Good solution [here.](https://leetcode.com/problems/as-far-from-land-as-possible/solutions/3167044/javascript-super-easy-to-understand/?orderBy=hot&languageTags=javascript)

## Solution

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var maxDistance = function (grid) {
  //Create an array containing two subarrays: the first subarray contains locations of water cells, the second one contains locations of land cells.
  let res = -1,
    n = grid.length,
    map = [[], []];
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      const p = grid[i][j];
      map[p].push([i, j]);
    }
  }
  if (map[0].length === 0 || map[1].length === 0) {
    return -1;
  }
  //Iterate through the first subarray. For each water cell, calculate the nearest distance to a land cell by looping through the second subarray.
  for (let i = 0; i < map[0].length; i++) {
    let nearest = 9999999;
    for (let j = 0; j < map[1].length; j++) {
      const d = distance(map[0][i], map[1][j]);
      if (d < nearest) {
        nearest = d;
      }
    }
    if (nearest > res) {
      res = nearest;
    }
  }
  return res;
};
//Get the maximum value of all nearest distance values.
const distance = (p0, p1) => {
  const x0 = p0[0],
    x1 = p1[0],
    y0 = p0[1],
    y1 = p1[1];
  let d = 0;
  if (x0 > x1) {
    d += x0 - x1;
  } else {
    d += x1 - x0;
  }
  if (y0 > y1) {
    d += y0 - y1;
  } else {
    d += y1 - y0;
  }
  return d;
};
```
