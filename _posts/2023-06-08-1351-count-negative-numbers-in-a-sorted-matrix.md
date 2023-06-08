---
layout: post
title: 1351. Count Negative Numbers in a Sorted Matrix
date: 2023-06-08 07:46 -0400
difficulty: easy
comments: true
---

Given a `m x n` matrix `grid` which is sorted in non-increasing order both row-wise and column-wise, return the number of negative numbers in `grid`.

## Example

```javascript
Input: grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
Output: 8
Explanation: There are 8 negatives number in the matrix.
```

## Solution

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var countNegatives = function (grid) {
  //return negative numbers in the grid
  if (grid.length === 0) return 0;
  let count = 0;
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      if (grid[i][j] < 0) {
        count++;
      }
    }
  }
  return count;
};
```
