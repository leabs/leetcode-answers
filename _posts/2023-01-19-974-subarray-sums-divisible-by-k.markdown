---
layout: post
title: "974. Subarray Sums Divisible by K"
date: 2023-01-19 07:35:33 -0500
comments: true
difficulty: medium
---

Given an integer array `nums` and an integer `k`, return the _number of non-empty subarrays that have a sum divisible by_ `k`.

A **subarray** is a **contiguous** part of an array.

<pre><strong>Input:</strong> nums = [4,5,0,-2,-3,1], k = 5
<strong>Output:</strong> 7
<strong>Explanation:</strong> There are 7 subarrays with a sum divisible by k = 5:
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]
</pre>

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var subarraysDivByK = function (A, K) {
  let freq = new Array(K).fill(0); // "moduloK : Times I've seen it so far"

  freq[0] = 1; //  Explained below

  // This is the accumulative sum of the elements of A
  let sum = 0;

  // The count of wanted subarrays, whose Sum%K= zero
  let count = 0;

  for (let i = 0; i < A.length; i++) {
    sum = sum + A[i];

    var remainder = sum % K;

    //ALWAYS CHOOSE THE POSITIVE REMAINDER
    if (remainder < 0) remainder += K; // Explained below

    count += freq[remainder];

    freq[remainder]++;
  }
  return count;
};
```
