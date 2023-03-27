---
layout: post
title: 64. Minimum Path Sum
date: 2023-03-27 08:29 -0400
difficulty: medium
comments: true
---

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-27.jpg" alt="Example tree image" />

```javascript
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

## Solution

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function (grid) {
  //For the length of the grid starting at 1, add the previous row's value to the current row's value
  for (let i = 1; i < grid.length; i++) {
    grid[i][0] += grid[i - 1][0];
  }
  //For the length of the grid starting at 1, add the previous column's value to the current column's value
  for (let i = 1; i < grid[0].length; i++) {
    grid[0][i] += grid[0][i - 1];
  }
  for (let i = 1; i < grid.length; i++) {
    for (let j = 1; j < grid[0].length; j++) {
      //Add the minimum of the previous row or previous column to the current value
      grid[i][j] += Math.min(grid[i - 1][j], grid[i][j - 1]);
    }
  }
  return grid[grid.length - 1][grid[0].length - 1];
};
```
