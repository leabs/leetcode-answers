---
layout: post
title: 1254. Number of Closed Islands
date: 2023-04-06 09:08 -0400
difficulty: medium
comments: true
---

Given a 2D grid consists of 0s (land) and 1s (water). An island is a maximal 4-directionally connected group of 0s and a closed island is an island totally (all left, top, right, bottom) surrounded by 1s.

Return the number of closed islands.

## Example

<img src="{{ site.baseurl }}/assets/images/apr-6.png" alt="Example grid image" />

```javascript
Input: grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
Output: 2
Explanation:
Islands in gray are closed because they are completely surrounded by water (group of 1s).
```

## Solution

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var closedIsland = function (grid) {
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
      grid[x][y] == 1
    ) {
      return;
    }
    //Mark as visited
    grid[x][y] = 1;
    dfs(x + 1, y, grid);
    dfs(x - 1, y, grid);
    dfs(x, y + 1, grid);
    dfs(x, y - 1, grid);
  }

  // Exclude connected group of 0s on the corners because they are not closed island.
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      //If 0 and on the edge, run dfs
      if (grid[i][j] == 0 && (i == 0 || i == m - 1 || j == 0 || j == n - 1)) {
        dfs(i, j, grid);
      }
    }
  }
  // Count the number of connected component of 0s on the grid.
  for (let i = 1; i < m - 1; i++) {
    for (let j = 1; j < n - 1; j++) {
      //If 0, increment count and run dfs
      if (grid[i][j] == 0) {
        dfs(i, j, grid);
        count++;
      }
    }
  }

  return count;
};
```
