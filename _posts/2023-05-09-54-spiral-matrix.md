---
layout: post
title: 54. Spiral Matrix
date: 2023-05-09 07:43 -0400
difficulty: medium
comments: true
---

Given an `m x n` `matrix`, return all elements of the `matrix` in spiral order.

## Example

<img src="{{ site.baseurl }}/assets/images/may-9.jpg" alt="Example grid image" />

```javascript
Input: matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];
Output: [1, 2, 3, 6, 9, 8, 7, 4, 5];
```

## Solution

```javascript
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function (matrix) {
  //Return an empty array if the matrix is empty.
  if (!matrix.length) return [];
  //Declare an array to store the spiral order.
  let spiral = [];
  //Declare the starting row and column.
  let rowStart = 0;
  let colStart = 0;
  //Declare the ending row and column.
  let rowEnd = matrix.length - 1;
  let colEnd = matrix[0].length - 1;
  //While the starting row is less than or equal to the ending row and the starting column is less than or equal to the ending column.
  while (rowStart <= rowEnd && colStart <= colEnd) {
    //Loop through the top row from left to right.
    for (let i = colStart; i <= colEnd; i++) {
      //Add the current element to the spiral array.
      spiral.push(matrix[rowStart][i]);
    }
    //Increment the starting row.
    rowStart++;
    //Loop through the right column from top to bottom.
    for (let i = rowStart; i <= rowEnd; i++) {
      //Add the current element to the spiral array.
      spiral.push(matrix[i][colEnd]);
    }
    //Decrement the ending column.
    colEnd--;
    //If the starting row is less than or equal to the ending row.
    if (rowStart <= rowEnd) {
      //Loop through the bottom row from right to left.
      for (let i = colEnd; i >= colStart; i--) {
        //Add the current element to the spiral array.
        spiral.push(matrix[rowEnd][i]);
      }
    }
    //Decrement the ending row.
    rowEnd--;
    //If the starting column is less than or equal to the ending column.
    if (colStart <= colEnd) {
      //Loop through the left column from bottom to top.
      for (let i = rowEnd; i >= rowStart; i--) {
        //Add the current element to the spiral array.
        spiral.push(matrix[i][colStart]);
      }
    }
    //Increment the starting column.
    colStart++;
  }
  //Return the spiral array.
  return spiral;
};
```
