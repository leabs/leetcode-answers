---
layout: post
title: 2352. Equal Row and Column Pairs
date: 2023-06-13 07:54 -0400
difficulty: medium
comments: true
---

Given a 0-indexed `n x n` integer matrix `grid`, return the number of pairs `(ri, cj)` such that row `ri` and column `cj` are equal.

A row and column pair is considered equal if they contain the same elements in the same order (i.e., an equal array).

## Example

<img src="{{ site.baseurl }}/assets/images/jun-13.jpg" alt="example grid image" width="300"/>

```javascript
Input: grid = [[3,2,1],[1,7,6],[2,7,7]]
Output: 1
Explanation: There is 1 equal row and column pair:
- (Row 2, Column 1): [2,7,7]
```

## Solution

Great solution [here](https://leetcode.com/problems/equal-row-and-column-pairs/solutions/3035336/easy-concise-javascript-solution/)

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var equalPairs = function (grid) {
  //Set rows and columns to empty arrays
  const rows = grid.map((arr) => arr.join());
  const columns = grid[0].map((col, i) => grid.map((row) => row[i]).join());
  //Set count to 0
  let count = 0;
  //Loop through rows and columns recursively
  for (let row of rows) {
    for (let column of columns) {
      //If row and column are equal, increment count
      if (row === column) count++;
    }
  }
  return count;
};
```
