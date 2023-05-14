---
layout: post
title: 1799. Maximize Score After N Operations
date: 2023-05-14 07:26 -0400
difficulty: hard
comments: true
---

You are given `nums`, an array of positive integers of size `2 * n`. You must perform `n` operations on this array.

In the `ith` operation (1-indexed), you will:

- Choose two elements, `x` and `y`.
- Receive a score of `i * gcd(x, y)`.
- Remove `x` and `y` from `nums`.

Return the maximum score you can receive after performing `n` operations.

The function `gcd(x, y)` is the greatest common divisor of `x` and `y`.

## Example

```javascript
Input: nums = [1,2]
Output: 1
Explanation: The optimal choice of operations is:
(1 * gcd(1, 2)) = 1
```

## Solution

Great solution found [here](https://leetcode.com/problems/maximize-score-after-n-operations/solutions/3522923/simple-javascript-solution/?languageTags=javascript)

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxScore = function (nums) {
  // cache to store the max score for each state
  const cache = new Map();
  // helper function to calculate gcd
  function gcd(a, b) {
    if (!b) return a;
    return gcd(b, a % b);
  }
  // helper function to calculate max score for each state
  function helper(arr, num, op) {
    if (!arr.length) return 0;
    const key = arr.join() + num;
    // if the state is already calculated, return the value
    if (cache.has(key)) return cache.get(key);
    let max = 0;
    for (let i = 0; i < arr.length; i++) {
      // for each element in the array, calculate the max score
      const nextArr = [...arr.slice(0, i), ...arr.slice(i + 1)];
      if (num) {
        const currGCD = gcd(num, arr[i]);
        const rest = helper(nextArr, null, op + 1);
        max = Math.max(max, op * currGCD + rest);
      } else {
        const rest = helper(nextArr, arr[i], op);
        max = Math.max(max, rest);
      }
    }
    // store the max score for the state
    cache.set(key, max);
    return max;
  }
  return helper(nums, null, 1);
};
```
