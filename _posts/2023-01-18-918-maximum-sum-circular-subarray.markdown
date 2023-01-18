---
layout: post
title: "918. Maximum Sum Circular Subarray"
date: 2023-01-18 07:35:33 -0500
comments: true
difficulty: medium
---

Given a circular integer array `nums` of length `n`, return the maximum possible sum of a non-empty subarray of `nums`.

A circular array means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A subarray may only include each element of the fixed buffer `nums` at most once. Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i <= k1, k2 <= j` with `k1 % n == k2 % n`.

<pre><strong>Input:</strong> nums = [1,-2,3,-2]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Subarray [3] has maximum sum 3.
</pre>

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubarraySumCircular = function (A) {
  //Declare vars
  let maxSum, max, minSum, min, total;
  //Set initial values
  maxSum = max = minSum = min = total = A[0];

  //Loop through array
  for (let i = 1; i < A.length; i++) {
    //Set n to current value
    const n = A[i];
    //Set max to the max of n or n + max
    max = Math.max(n, n + max);
    //Set maxSum to the max of max or maxSum
    maxSum = Math.max(max, maxSum);
    //Set min to the min of n or n + min
    min = Math.min(n, n + min);
    //Set minSum to the min of min or minSum
    minSum = Math.min(min, minSum);
    //Add n to total
    total += n;
  }
  //Return maxSum if greater than 0, otherwise return maxSum
  return maxSum > 0 ? Math.max(maxSum, total - minSum) : maxSum;
};
```
