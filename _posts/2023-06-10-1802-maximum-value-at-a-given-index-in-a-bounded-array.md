---
layout: post
title: 1802. Maximum Value at a Given Index in a Bounded Array
date: 2023-06-10 07:41 -0400
difficulty: medium
comments: true
---

You are given three positive integers: `n`, `index`, and `maxSum`. You want to construct an array `nums` (0-indexed) that satisfies the following conditions:

- `nums.length == n`
- `nums[i]` is a positive integer where `0 <= i < n`.
- `abs(nums[i] - nums[i+1]) <= 1` where `0 <= i < n-1`.
- The sum of all the elements of nums does not exceed maxSum.
- `nums[index]` is maximized.

Return `nums[index]` of the constructed array.

Note that `abs(x)` equals `x` if `x >= 0`, and `-x` otherwise.

## Example

```javascript
Input: n = 4, index = 2,  maxSum = 6
Output: 2
Explanation: nums = [1,2,2,1] is one array that satisfies all the conditions.
There are no arrays that satisfy all the conditions and have nums[2] == 3, so 2 is the maximum nums[2].
```

## Solution

Great solution found [here](https://leetcode.com/problems/maximum-value-at-a-given-index-in-a-bounded-array/solutions/3621422/simple-javascript-solution/)

```javascript
/**
 * @param {number} n
 * @param {number} index
 * @param {number} maxSum
 * @return {number}
 */
var maxValue = function (n, index, maxSum) {
  //Set the min and max values
  let min = Math.floor(maxSum / n);
  let max = maxSum;
  //Find the sum of the left and right side of the array
  const findSum = (num, len) => {
    //If the length is less than the number, return the sum of the first n numbers
    if (len < num) return (len * (num + num - len + 1)) / 2;
    //Return the sum of the first n numbers plus the remaining numbers
    return (num * (num + 1)) / 2 + (len - num);
  };
  //Helper function to check if the sum of the left and right side of the array is greater than the maxSum
  const helper = (num) => {
    //Find the sum of the left and right side of the array
    const leftSum = findSum(num, index + 1);
    const rightSum = findSum(num, n - index);
    //Return true if the sum of the left and right side of the array is greater than the maxSum
    return maxSum >= leftSum + rightSum - num;
  };
  while (min <= max) {
    const mid = (min + max) >> 1;
    helper(mid) ? (min = mid + 1) : (max = mid - 1);
  }
  return max;
};
```
