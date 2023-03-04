---
layout: post
title: 2444. Count Subarrays With Fixed Bounds
date: 2023-03-04 08:14 -0500
difficulty: hard
comments: true
---

You are given an integer array `nums` and two integers `minK` and `maxK`.

A fixed-bound subarray of `nums` is a subarray that satisfies the following conditions:

- The **minimum** value in the subarray is equal to `minK`.
- The **maximum** value in the subarray is equal to `maxK`.

Return the number of fixed-bound subarrays.

A **subarray** is a **contiguous** part of an array.

## Example

```javascript
Input: nums = [1,3,5,2,7,5], minK = 1, maxK = 5
Output: 2
Explanation: The fixed-bound subarrays are [1,3,5] and [1,3,5,2].
```

## Solution

Great solution found [here](https://leetcode.com/problems/count-subarrays-with-fixed-bounds/solutions/3255114/very-easy-100-easiest-logic-ever-fully-explained-step-by-step-c-javascript-java-python/?orderBy=hot&languageTags=javascript)

```javascript
/**
 * @param {number[]} nums
 * @param {number} minK
 * @param {number} maxK
 * @return {number}
 */
var countSubarrays = function (nums, minK, maxK) {
  let sum = 0;
  let start = 0,
    minStart = 0,
    maxStart = 0;
  let minf = false,
    maxf = false;

  for (let i = 0; i < nums.length; i++) {
    let num = nums[i];
    // If the current number is not within the bounds, reset the start index
    if (num < minK || num > maxK) {
      minf = false;
      maxf = false;
      start = i + 1;
    }
    // If the current number is equal to the minimum or maximum, set the start index
    if (num === minK) {
      minf = true;
      minStart = i;
    }
    // If the current number is equal to the minimum or maximum, set the start index
    if (num === maxK) {
      maxf = true;
      maxStart = i;
    }
    // If both the minimum and maximum have been found, add the number of subarrays to the sum
    if (minf && maxf) {
      sum += Math.min(minStart, maxStart) - start + 1;
    }
  }

  return sum;
};
```
