---
layout: post
title: 1539. Kth Missing Positive Number
date: 2023-03-06 07:47 -0500
difficulty: easy
comments: true
---

Given an array `arr` of positive integers sorted in a **strictly increasing order, and an integer** `k`.

Return the `kth` **positive** integer that is **missing** from this array.

## Example

```javascript
Input: arr = [2,3,4,7,11], k = 5
Output: 9
Explanation: The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.
```

## Solution

```javascript
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number}
 */
var findKthPositive = function (arr, k) {
  // create a set of all the numbers in the array
  const set = new Set(arr);
  // create a variable to keep track of the number of missing numbers
  let missing = 0;
  // create a variable to keep track of the current number
  let current = 1;
  // loop through the numbers until we find the kth missing number
  while (missing < k) {
    // if the current number is not in the set, increment the missing variable
    if (!set.has(current)) {
      missing++;
    }
    // increment the current number
    current++;
  }
  // return the current number
  return current - 1;
};
```
