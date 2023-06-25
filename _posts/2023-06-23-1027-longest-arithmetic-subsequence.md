---
layout: post
title: 1027. Longest Arithmetic Subsequence
date: 2023-06-23 08:49 -0400
difficulty: medium
comments: true
---

Given an array `nums` of integers, return the length of the longest arithmetic subsequence in `nums`.

Note that:

- A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.
- A sequence `seq` is arithmetic if `seq[i + 1] - seq[i]` are all the same value (for `0 <= i < seq.length - 1`).

## Example

```javascript
Input: nums = [3,6,9,12]
Output: 4
Explanation:  The whole array is an arithmetic sequence with steps of length = 3.
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestArithSeqLength = function (nums) {
  // The length of the input array.
  let n = nums.length;
  // If the array is empty, the answer is 0.
  if (n === 0) {
    return 0;
  }
  // If the array has only one element, the answer is 1.
  if (n === 1) {
    return 1;
  }
  // dp[i] is a map whose key is the difference and value is the
  // length of the longest arithmetic sequence ending at index i.
  let dp = new Array(n);
  // The length of the longest arithmetic sequence so far.
  max = 2;
  // Iterate over the array from left to right.
  for (let i = 0; i < n; i++) {
    // Initialize dp[i] as an empty map.
    dp[i] = new Map();
    // Iterate over the array from left to i.
    for (let j = 0; j < i; j++) {
      // The difference between nums[i] and nums[j].
      let diff = nums[i] - nums[j];
      // The length of the longest arithmetic sequence ending at index j.
      let count = dp[j].get(diff) || 1;
      // The length of the longest arithmetic sequence ending at index i.
      dp[i].set(diff, Math.max(dp[i].get(diff) || 0, count + 1));
      // Update max.
      max = Math.max(max, dp[i].get(diff));
    }
  }
  return max;
};
```
