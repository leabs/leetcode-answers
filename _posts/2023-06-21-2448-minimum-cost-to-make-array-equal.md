---
layout: post
title: 2448. Minimum Cost to Make Array Equal
date: 2023-06-21 08:49 -0400
difficulty: hard
comments: true
---

You are given two **0-indexed** arrays `nums` and `cost` consisting each of `n` **positive** integers.

You can do the following operation any number of times:

- Increase or decrease any element of the array `nums` by `1`.

The cost of doing one operation on the `ith` element is `cost[i]`.

Return the minimum total cost such that all the elements of the array `nums` become equal.

## Example

```javascript
Input: nums = [1,3,5,2], cost = [2,3,1,14]
Output: 8
Explanation: We can make all the elements equal to 2 in the following way:
- Increase the 0th element one time. The cost is 2.
- Decrease the 1st element one time. The cost is 3.
- Decrease the 2nd element three times. The cost is 1 + 1 + 1 = 3.
The total cost is 2 + 3 + 3 = 8.
It can be shown that we cannot make the array equal with a smaller cost.
```

## Solution

Great solution found [here](https://leetcode.com/problems/minimum-cost-to-make-array-equal/solutions/3664875/short-simple-crisp-js-solution/)

```javascript
/**
 * @param {number[]} nums
 * @param {number[]} cost
 * @return {number}
 */
var minCost = function (nums, cost) {
  //Set n to the length of nums
  const n = nums.length;
  //If n is less than or equal to 1, return 0
  if (n <= 1) return 0;
  // Declare an array arr
  let arr = [];
  //Loop through nums
  for (let i = 0; i < n; i++) arr[i] = [nums[i], cost[i]];
  //Sort arr by the first element
  arr.sort((a, b) => a[0] - b[0]);
  //Declare an array psum
  let psum = [arr[0][1]];
  //Loop through arr to populate psum
  for (let i = 1; i < n; i++) psum.push(psum[i - 1] + arr[i][1]);
  //Declare sum and set it to 0
  let sum = 0;
  //Loop through arr to find the sum
  for (let i = 1; i < n; i++) {
    sum += Math.abs(arr[i][0] - arr[0][0]) * arr[i][1];
  }
  //Declare ans and set it to Infinity
  let ans = Infinity;
  //Loop through arr to find the minimum sum
  ans = Math.min(ans, sum);
  //Loop through arr to find ans using psum
  for (let i = 1; i < n; i++) {
    sum += psum[i - 1] * (arr[i][0] - arr[i - 1][0]);
    sum -= (psum[n - 1] - psum[i - 1]) * (arr[i][0] - arr[i - 1][0]);
    ans = Math.min(ans, sum);
  }
  return ans;
};
```
