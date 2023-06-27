---
layout: post
title: 373. Find K Pairs with Smallest Sums
date: 2023-06-27 09:21 -0400
difficulty: medium
comments: true
---

You are given two integer arrays `nums1` and `nums2` sorted in ascending order and an integer `k`.

Define a pair `(u, v)` which consists of one element from the first array and one element from the second array.

Return the `k` pairs `(u1, v1), (u2, v2), ..., (uk, vk)` with the smallest sums.

## Example

```javascript
Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
Output: [[1,2],[1,4],[1,6]]
Explanation: The first 3 pairs are returned from the sequence: [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```

## Solution

Great solution [here](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/solutions/861173/javascript-solution-array-of-objects-with-comments-beat-90-68/)

```javascript
var kSmallestPairs = function (nums1, nums2, k) {
  if (nums1.length === 0 || nums2.length === 0) return [];

  let arr = [];
  let max = -Infinity;

  for (let i = 0; i < nums1.length; i++) {
    for (let j = 0; j < nums2.length; j++) {
      let obj = {
        sum: nums1[i] + nums2[j],
        nums: [nums1[i], nums2[j]],
      };

      if (obj.sum >= max && arr.length >= k) {
        break;
      } else if (obj.sum <= max && arr.length < k) {
        arr.push(obj);
      } else if (obj.sum > max && arr.length < k) {
        max = obj.sum;
        arr.push(obj);
      } else if (obj.sum < max && arr.length >= k) {
        let newMax = -Infinity;
        let replaced = false;
        for (let n = 0; n < arr.length; n++) {
          if (!replaced && arr[n].sum === max) {
            arr[n] = obj;
            replaced = true;
          }
          if (arr[n].sum > newMax) newMax = arr[n].sum;
        }
        max = newMax;
      }
    }
  }

  return arr.map((obj) => obj.nums);
};
```
