---
layout: post
title: 2328. Number of Increasing Paths in a Grid
date: 2023-06-18 09:28 -0400
difficulty: hard
comments: true
---

You are given an `m x n` integer matrix `grid`, where you can move from a cell to any adjacent cell in all `4` directions.

Return the number of strictly increasing paths in the grid such that you can start from any cell and end at any cell. Since the answer may be very large, return it modulo `109 + 7`.

Two paths are considered different if they do not have exactly the same sequence of visited cells.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-18.png" alt="example grid image" width="300"/>

```javascript
Input: grid = [[1,1],[3,4]]
Output: 8
Explanation: The strictly increasing paths are:
- Paths with length 1: [1], [1], [3], [4].
- Paths with length 2: [1 -> 3], [1 -> 4], [3 -> 4].
- Paths with length 3: [1 -> 3 -> 4].
The total number of paths is 4 + 3 + 1 = 8.
```

## Solution

Great solution found [here]()

```javascript
var countPaths = function (grid) {
  //Set up variables
  let mod = Math.pow(10, 9) + 7;
  let result = 0;
  let rows = grid.length,
    columns = grid[0].length;
  //Create a dp array
  let dp = Array(rows)
    .fill(null)
    .map((_) => Array(columns).fill(0));
  //DFS function that returns the number of paths
  const dfs = (r, c, preVal) => {
    if (r < 0 || r == rows || c < 0 || c == columns || grid[r][c] <= preVal)
      return 0;
    if (dp[r][c]) return dp[r][c];
    return (dp[r][c] =
      (1 +
        dfs(r + 1, c, grid[r][c]) +
        dfs(r - 1, c, grid[r][c]) +
        dfs(r, c + 1, grid[r][c]) +
        dfs(r, c - 1, grid[r][c])) %
      mod);
  };
  //Recursive call to dfs
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < columns; j++) {
      result += dfs(i, j, -1) % mod;
    }
  }

  return result % mod;
};
```
