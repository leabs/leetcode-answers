---
layout: post
title: 59. Spiral Matrix II
date: 2023-05-10 08:59 -0400
difficulty: medium
comments: true
---

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

## Example

<img src="{{ site.baseurl }}/assets/images/may-10.jpg" alt="Example grid image" />

```javascript
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

## Solution

```javascript
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    //Variables to declare and to make life easier
    let spiral = [];
    let rowStart = 0;
    let colStart = 0;
    let rowEnd = n - 1;
    let colEnd = n - 1;
    let num = 1;

    //While the starting row is less than or equal to the ending row and the starting column is less than or equal to the ending column.
    while (rowStart <= rowEnd && colStart <= colEnd) {
        //Loop through the top row from left to right.
        for (let i = colStart; i <= colEnd; i++) {
            //Add the current element to the spiral array.
            spiral[rowStart] = spiral[rowStart] || [];
            //Add the current number to the spiral array.
            spiral[rowStart][i] = num++;
        }
        //Increment the starting row.
        rowStart++;
        for (let i = rowStart; i <= rowEnd; i++) {
            //Add the current element to the spiral array.
            spiral[i] = spiral[i] || [];
            //Add the current number to the spiral array.
            spiral[i][colEnd] = num++;
        }
        //Decrement the ending column.
        colEnd--;
        //If the starting row is less than or equal to the ending row.
        if (rowStart <= rowEnd) {
            for (let i = colEnd; i >= colStart; i--) {
                //Add the current element to the spiral array.
                spiral[rowEnd] = spiral[rowEnd] || [];
                //Add the current number to the spiral array.
                spiral[rowEnd][i] = num++;
            }
            //Decrement the ending row.
            rowEnd--;
        }
        if (colStart <= colEnd) {
            //Loop through the bottom row from right to left.
            for (let i = rowEnd; i >= rowStart; i--) {
                //Add the current element to the spiral array.
                spiral[i] = spiral[i] || [];
                //Add the current number to the spiral array.
                spiral[i][colStart] = num++;
            }
            //Increment the starting column.
            colStart++;
        }
    }
    return spiral;
};
```
