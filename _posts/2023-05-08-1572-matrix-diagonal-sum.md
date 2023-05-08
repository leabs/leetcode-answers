---
layout: post
title: 1572. Matrix Diagonal Sum
date: 2023-05-08 07:43 -0400
difficulty: easy
comments: true
---

Given a square matrix `mat`, return the sum of the matrix diagonals.

Only include the sum of all the elements on the primary diagonal and all the elements on the secondary diagonal that are not part of the primary diagonal.

## Example

<img src="{{ site.baseurl }}/assets/images/may-8.png" alt="Example grid image" />

```javascript
Input: mat = [[1,2,3],
              [4,5,6],
              [7,8,9]]
Output: 25
Explanation: Diagonals sum: 1 + 5 + 9 + 3 + 7 = 25
Notice that element mat[1][1] = 5 is counted only once.
```

## Solution

```javascript
/**
 * @param {number[][]} mat
 * @return {number}
 */
var diagonalSum = function (mat) {
  //declare sum variable
  let sum = 0;
  //find the middle of the matrix from the length of the matrix
  let middle = Math.floor(mat.length / 2);
  //for loop to iterate through the matrix
  for (let i = 0; i < mat.length; i++) {
    //add the sum of the primary diagonal
    sum += mat[i][i];
    //add the sum of the secondary diagonal
    sum += mat[i][mat.length - 1 - i];
  }
  //if the matrix length is odd
  if (mat.length % 2 !== 0) {
    //subtract the middle value from the sum
    sum -= mat[middle][middle];
  }
  //return the sum
  return sum;
};
```
