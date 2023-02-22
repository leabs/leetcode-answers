---
layout: post
title: 540. Single Element in a Sorted Array
date: 2023-02-21 08:27 -0500
difficulty: medium
comments: true
---

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return the single element that appears only once.

Your solution must run in `O(log n)` time and `O(1)` space.

## Example

```javascript
Input: nums = [1, 1, 2, 3, 3, 4, 4, 8, 8];
Output: 2;
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNonDuplicate = function (nums) {
  // Loop through nums to identify the single element.
  for (let i = 0; i < nums.length; i++) {
    // If the current element is not equal to the next element, return the current element.
    if (nums[i] != nums[i + 1]) {
      return nums[i];
    }
    // If the current element is equal to the next element, skip the next element.
    i++;
  }
};
```
