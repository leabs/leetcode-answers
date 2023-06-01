---
layout: post
title: 1091. Shortest Path in Binary Matrix
date: 2023-06-01 07:43 -0400
difficulty: medium
comments: true
---

Given an `n x n` binary matrix `grid`, return the length of the shortest clear path in the matrix. If there is no clear path, return `-1`.

A clear path in a binary matrix is a path from the top-left cell (i.e., `(0, 0)`) to the bottom-right cell (i.e., `(n - 1, n - 1)`) such that:

- All the visited cells of the path are `0`.
- All the adjacent cells of the path are 8-directionally connected (i.e., they are different and they share an edge or a corner).

The length of a clear path is the number of visited cells of this path.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-1.png" alt="matrix image" width="300"/>

```javascript
Input: grid = [
  [0, 1],
  [1, 0],
];
Output: 2;
```

## Solution

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var shortestPathBinaryMatrix = function (grid) {
  //Declare the length of the grid
  const n = grid.length;
  //If the first cell is blocked, return -1
  if (grid[0][0] === 1) return -1;
  //If the last cell is blocked, return -1
  if (grid[n - 1][n - 1] === 1) return -1;
  //Declare the queue
  const queue = [[0, 0]];
  //Declare the directions
  const directions = [
    [0, 1],
    [0, -1],
    [1, 0],
    [-1, 0],
    [1, 1],
    [1, -1],
    [-1, 1],
    [-1, -1],
  ];
  //Declare the distance
  let distance = 0;
  //While the queue is not empty
  while (queue.length) {
    //Increment the distance
    distance++;
    //Declare the length of the queue
    const len = queue.length;
    //Iterate the queue
    for (let i = 0; i < len; i++) {
      //Declare the current cell
      const [row, col] = queue.shift();
      //If the current cell is the last cell, return the distance
      if (row === n - 1 && col === n - 1) return distance;
      //Iterate the directions
      for (const [x, y] of directions) {
        //Declare the next row and column
        const nextRow = row + x;
        const nextCol = col + y;
        //If the next row and column are out of bounds, continue
        if (nextRow < 0 || nextRow >= n || nextCol < 0 || nextCol >= n)
          continue;
        //If the next cell is not 0, continue
        if (grid[nextRow][nextCol] !== 0) continue;
        //Mark the next cell as visited
        grid[nextRow][nextCol] = 1;
        //Add the next cell to the queue
        queue.push([nextRow, nextCol]);
      }
    }
  }
  //Return -1
  return -1;
};
```
