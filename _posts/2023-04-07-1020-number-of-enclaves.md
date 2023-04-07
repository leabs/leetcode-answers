---
layout: post
title: 1020. Number of Enclaves
date: 2023-04-07 08:06 -0400
difficulty: medium
comments: true
---

You are given an `m x n` binary matrix `grid`, where `0` represents a sea cell and `1` represents a land cell.

A **move** consists of walking from one land cell to another adjacent (4-directionally) land cell or walking off the boundary of the `grid`.

Return _the number of land cells in `grid` for which we cannot walk off the boundary of the grid in any number of **moves**_.

## Example

<img src="{{ site.baseurl }}/assets/images/apr-7.jpg" alt="Example grid image" />

```javascript
Input: grid = [[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]
Output: 3
Explanation: There are three 1s that are enclosed by 0s, and one 1 that is not enclosed because its on the boundary.
```

## Solution

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var numEnclaves = function (grid) {
  //Assign count, rows, and cols
  let m = grid.length;
  let n = grid[0].length;
  let count = 0;
  //Function to check if island is closed
  function dfs(x, y, grid) {
    if (
      x < 0 ||
      x >= grid.length ||
      y < 0 ||
      y >= grid[0].length ||
      grid[x][y] == 0
    ) {
      return;
    }
    //Mark as visited
    grid[x][y] = 0;
    dfs(x + 1, y, grid);
    dfs(x - 1, y, grid);
    dfs(x, y + 1, grid);
    dfs(x, y - 1, grid);
  }

  // Exclude connected group of 0s on the corners because they are not closed island.
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      //If 0 and on the edge, run dfs
      if (grid[i][j] == 1 && (i == 0 || i == m - 1 || j == 0 || j == n - 1)) {
        dfs(i, j, grid);
      }
    }
  }

  //Count remaining 1s
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (grid[i][j] == 1) {
        count++;
      }
    }
  }
  return count;
};
```
