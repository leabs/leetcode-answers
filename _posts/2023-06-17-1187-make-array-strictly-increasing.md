---
layout: post
title: 1187. Make Array Strictly Increasing
date: 2023-06-17 09:10 -0400
difficulty: hard
comments: true
---

Given two integer arrays `arr1` and `arr2`, return the minimum number of operations (possibly zero) needed to make `arr1` strictly increasing.

In one operation, you can choose two indices `0 <= i < arr1.lengt`h and `0 <= j < arr2.length` and do the assignment `arr1[i] = arr2[j]`.

If there is no way to make `arr1` strictly increasing, return `-1`.

## Example

```javascript
Input: arr1 = [1,5,3,6,7], arr2 = [1,3,2,4]
Output: 1
Explanation: Replace 5 with 2, then arr1 = [1, 2, 3, 6, 7].
```

## Solution

Great solution found [here](https://leetcode.com/problems/make-array-strictly-increasing/solutions/3646782/simple-javascript-solution/)

```javascript
/**
 * @param {number[]} arr1
 * @param {number[]} arr2
 * @return {number}
 */

var makeArrayIncreasing = function (arr1, arr2) {
  // Sort arr2
  arr2.sort((a, b) => a - b);
  // Create a map of arr2
  const binarySearch = (arr, target) => {
    let l = 0,
      r = arr.length,
      mid;
    while (l < r) {
      mid = (l + r) >> 1;
      arr[mid] > target ? (r = mid) : (l = ++mid);
    }
    return l;
  };
  // DFS function to find the minimum number of changes
  const dfs = (i, prev) => {
    if (i >= arr1.length) return 0;
    let key = `${i},${prev}`;
    if (key in memo) return memo[key];
    let j = binarySearch(arr2, prev);
    let swap = j < arr2.length ? 1 + dfs(i + 1, arr2[j]) : Infinity;
    let noSwap = arr1[i] > prev ? dfs(i + 1, arr1[i]) : Infinity;
    return (memo[key] = Math.min(swap, noSwap));
  };
  const memo = {};
  const changes = dfs(0, -Infinity);
  // Return -1 if changes is Infinity
  return changes === Infinity ? -1 : changes;
};
```
