---
layout: post
title: "944. Delete Columns to Make Sorted"
date: 2023-01-03 10:35:33 -0500
---

You are given an array of `n` strings `strs`, all of the same length.

The strings can be arranged such that there is one on each line, making a grid. For example, `strs = ["abc", "bce", "cae"]` can be arranged as:

```
abc
bce
cae
```

You want to delete the columns that are not sorted lexicographically. In the above example (0-indexed), columns 0 ('a', 'b', 'c') and 2 ('c', 'e', 'e') are sorted while column 1 ('b', 'c', 'a') is not, so you would delete column 1.

Return the number of columns that you will delete.

```javascript
/**
 * @param {string[]} strs
 * @return {number}
 */
var minDeletionSize = function (strs) {
  //set count to 0
  let count = 0;
  //for loop to iterate through the strs array
  for (let i = 0; i < strs[0].length; i++) {
    //for loop to iterate through the strs array
    for (let j = 0; j < strs.length - 1; j++) {
      //if the strs array at j is greater than the strs array at j + 1
      if (strs[j][i] > strs[j + 1][i]) {
        //increment count
        count++;
        //break
        break;
      }
    }
  }
  return count;
};
```
