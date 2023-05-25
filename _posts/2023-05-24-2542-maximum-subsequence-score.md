---
layout: post
title: 2542. Maximum Subsequence Score
date: 2023-05-24 08:03 -0400
difficulty: medium
comments: true
---

You are given two 0-indexed integer arrays `nums1` and `nums2` of equal length `n` and a positive integer `k`. You must choose a subsequence of indices from `nums1` of length `k`.

For chosen indices `i0`, `i1`, ..., `ik - 1`, your score is defined as:

-The sum of the selected elements from `nums1` multiplied with the minimum of the selected elements from `nums2`.

- It can defined simply as: `(nums1[i0] + nums1[i1] +...+ nums1[ik - 1]) * min(nums2[i0] , nums2[i1], ... ,nums2[ik - 1])`.
  Return the maximum possible score.

A subsequence of indices of an array is a set that can be derived from the set `{0, 1, ..., n-1}` by deleting some or no elements.

## Example

```javascript
Input: nums1 = [1,3,3,2], nums2 = [2,1,3,4], k = 3
Output: 12
Explanation:
The four possible subsequence scores are:
- We choose the indices 0, 1, and 2 with score = (1+3+3) * min(2,1,3) = 7.
- We choose the indices 0, 1, and 3 with score = (1+3+2) * min(2,1,4) = 6.
- We choose the indices 0, 2, and 3 with score = (1+3+2) * min(2,3,4) = 12.
- We choose the indices 1, 2, and 3 with score = (3+3+2) * min(1,3,4) = 8.
Therefore, we return the max score, which is 12.
```

## Solution

Great solution found [here](https://leetcode.com/problems/maximum-subsequence-score/solutions/3557264/heap-python-js-solution/)

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number}
 */
var maxScore = function (nums1, nums2, k) {
  //Declare result, totalSum, and a heap
  let result = 0;
  let totalSum = 0;
  let heap = new MinPriorityQueue({ priority: (element) => element });

  //Merge the two arrays
  const merged = nums1.map((nums1Val, i) => [nums2[i], nums1Val]);
  //Sort the merged array
  merged.sort((a, b) => b[0] - a[0]);

  //For each element in the merged array
  for (const [maxOf2, num1Val] of merged) {
    //If the heap size is equal to k
    if (heap.size() === k) {
      //Remove the first element from the heap
      totalSum -= heap.dequeue().element;
    }
    //Add the num1Val to the totalSum
    totalSum += num1Val;
    //Add the num1Val to the heap
    heap.enqueue(num1Val);
    //Update the result
    if (heap.size() === k) {
      //Update the result
      result = Math.max(result, totalSum * maxOf2);
    }
  }
  return result;
};
```
