---
layout: post
title: 704. Binary Search
date: 2023-04-01 08:47 -0400
difficulty: easy
comments: true
---

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

## Example

```javascript
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {
  // set left to 0
  let left = 0;
  // set right to nums length - 1
  let right = nums.length - 1;
  // while left is less than or equal to right
  while (left <= right) {
    // set middle to left plus right divided by 2
    let middle = Math.floor((left + right) / 2);
    // if target is equal to middle
    if (target === nums[middle]) {
      // return middle
      return middle;
      // else if target is less than middle
    } else if (target < nums[middle]) {
      // set right to middle - 1
      right = middle - 1;
      // else
    } else {
      // set left to middle + 1
      left = middle + 1;
    }
  }
  // return -1
  return -1;
};
```
