---
layout: post
title: 1498. Number of Subsequences That Satisfy the Given Sum Condition
date: 2023-05-06 10:13 -0400
difficulty: medium
comments: true
---

You are given an array of integers `nums` and an integer `target`.

Return the number of non-empty subsequences of `nums` such that the sum of the minimum and maximum element on it is less or equal to `target`. Since the answer may be too large, return it modulo `109 + 7`.

## Example

```javascript
Input: nums = [3,5,6,7], target = 9
Output: 4
Explanation: There are 4 subsequences that satisfy the condition.
[3] -> Min value + max value <= target (3 + 3 <= 9)
[3,5] -> (3 + 5 <= 9)
[3,5,6] -> (3 + 6 <= 9)
[3,6] -> (3 + 6 <= 9)
```

## Solution

Good solution [here](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/solutions/3492836/best-javascript-solution/?orderBy=most_votes&languageTags=javascript).

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var numSubseq = function (nums, target) {
  const mod = 1000000007,
    arr = [];
  let num = 1;

  for (let i = 0; i < nums.length; i++) {
    arr.push(num);
    //num set to modulous of num * 2
    num = (num * 2) % mod;
  }
  //Sort nums array
  nums.sort((a, b) => a - b);

  let count = 0,
    j = nums.length - 1;

  for (let i = 0; i < nums.length && nums[i] * 2 <= target; i++) {
    while (j && nums[j] + nums[i] > target) j--;
    //count set to modulous of count + arr[j - i]
    count = (count + arr[j - i]) % mod;
  }
  return count;
};
```
