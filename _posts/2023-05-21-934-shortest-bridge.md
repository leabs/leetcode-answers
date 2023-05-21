---
layout: post
title: 934. Shortest Bridge
date: 2023-05-21 09:04 -0400
difficulty: medium
comments: true
---

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

An island is a 4-directionally connected group of 1's not connected to any other 1's. There are **exactly two islands** in `grid`.

You may change `0`'s to `1`'s to connect the two islands to form one island.

Return the smallest number of `0`'s you must flip to connect the two islands.

## Example

```javascript
Input: grid = [
  [0, 1],
  [1, 0],
];
Output: 1;
```

## Solution

Great solution found [here](https://leetcode.com/problems/shortest-bridge/solutions/3547387/beats-95-explained-js-using-bfs-and-dfs/)

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */

const DIRECTIONS = [
  [-1, 0],
  [1, 0],
  [0, -1],
  [0, 1],
];

var shortestBridge = function (grid) {
  const rows = grid.length;
  const cols = grid[0].length;

  let queue = [];

  const exploreIslandDFS = (row, col) => {
    //If row or col is less than 0 or row or col is greater than or equal to rows or cols or grid[row][col] is not equal to 1
    if (
      row < 0 ||
      row >= rows ||
      col < 0 ||
      col >= cols ||
      grid[row][col] !== 1
    ) {
      return false;
    }
    queue.push([row, col]);
    grid[row][col] = 2;

    exploreIslandDFS(row - 1, col);
    exploreIslandDFS(row + 1, col);
    exploreIslandDFS(row, col - 1);
    exploreIslandDFS(row, col + 1);

    return true;
  };

  const buildBridgeBFS = () => {
    let distance = -1;
    let currentQueue = [];

    while (queue.length) {
      currentQueue = queue;
      queue = [];

      for (let [row, col] of currentQueue) {
        for (let [dx, dy] of DIRECTIONS) {
          const nextRow = row + dx;
          const nextCol = col + dy;

          if (
            nextRow >= 0 &&
            nextRow < rows &&
            nextCol >= 0 &&
            nextCol < cols &&
            grid[nextRow][nextCol] !== 2
          ) {
            if (grid[nextRow][nextCol] === 1) {
              return distance + 1;
            }

            queue.push([nextRow, nextCol]);
            grid[nextRow][nextCol] = 2;
          }
        }
      }

      distance++;
    }

    return -1;
  };

  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (exploreIslandDFS(i, j)) {
        return buildBridgeBFS();
      }
    }
  }

  return -1;
};
```
