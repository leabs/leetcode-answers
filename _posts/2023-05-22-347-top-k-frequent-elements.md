---
layout: post
title: 347. Top K Frequent Elements
date: 2023-05-22 08:56 -0400
difficulty: medium
comments: true
---

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in **any order**.

## Example

```javascript
Input: (nums = [1, 1, 1, 2, 2, 3]), (k = 2);
Output: [1, 2];
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var topKFrequent = function (nums, k) {
  //Create a map
  let map = new Map();
  //FOR the length of nums
  for (let i = 0; i < nums.length; i++) {
    //IF the map has nums at i
    if (map.has(nums[i])) {
      //Increment the map at nums at i
      map.set(nums[i], map.get(nums[i]) + 1);
    } else {
      //ELSE set the map at nums at i to 1
      map.set(nums[i], 1);
    }
  }
  //Create a result array
  let result = [];
  //Create a sorted array
  let sorted = [...map.entries()].sort((a, b) => b[1] - a[1]);
  //FOR the length of k
  for (let i = 0; i < k; i++) {
    //Push the sorted at i at 0 to the result
    result.push(sorted[i][0]);
  }
  //Return the result
  return result;
};
```
