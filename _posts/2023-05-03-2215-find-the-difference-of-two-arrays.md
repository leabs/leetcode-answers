---
layout: post
title: 2215. Find the Difference of Two Arrays
date: 2023-05-03 08:52 -0400
difficulty: easy
comments: true
---

Given two **0-indexed** integer arrays `nums1` and `nums2`, return a list `answer` of size `2` where:

- `answer[0]` is a list of all **distinct** integers in `nums1` which are **not** present in `nums2`.
- `answer[1]` is a list of all **distinct** integers in `nums2` which are not present in `nums1`.

**Note** that the integers in the lists may be returned in **any** order.

## Example

```javascript
Input: nums1 = [1,2,3], nums2 = [2,4,6]
Output: [[1,3],[4,6]]
Explanation:
For nums1, nums1[1] = 2 is present at index 0 of nums2, whereas nums1[0] = 1 and nums1[2] = 3 are not present in nums2. Therefore, answer[0] = [1,3].
For nums2, nums2[0] = 2 is present at index 1 of nums1, whereas nums2[1] = 4 and nums2[2] = 6 are not present in nums2. Therefore, answer[1] = [4,6].
```

## Solution

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[][]}
 */
var findDifference = function (nums1, nums2) {
  //Declare a new array to store the result along with set1 and set2
  let res = [[], []];
  let set1 = new Set(nums1);
  let set2 = new Set(nums2);
  //Loop through set1 and check if set2 has the same value
  for (let num of set1) {
    //If not, push the value to the result array
    if (!set2.has(num)) {
      //Push the value to the result array
      res[0].push(num);
    }
  }
  //Loop through set2 and check if set1 has the same value
  for (let num of set2) {
    //If not, push the value to the result array
    if (!set1.has(num)) {
      //Push the value to the result array
      res[1].push(num);
    }
  }
  return res;
};
```
