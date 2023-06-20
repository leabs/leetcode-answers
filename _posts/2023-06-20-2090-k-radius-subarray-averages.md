---
layout: post
title: 2090. K Radius Subarray Averages
date: 2023-06-20 08:32 -0400
difficulty: medium
comments: true
---

You are given a 0-indexed array nums of n integers, and an integer k.

The k-radius average for a subarray of nums centered at some index i with the radius k is the average of all elements in nums between the indices i - k and i + k (inclusive). If there are less than k elements before or after the index i, then the k-radius average is -1.

Build and return an array avgs of length n where avgs[i] is the k-radius average for the subarray centered at index i.

The average of x elements is the sum of the x elements divided by x, using integer division. The integer division truncates toward zero, which means losing its fractional part.

For example, the average of four elements 2, 3, 1, and 5 is (2 + 3 + 1 + 5) / 4 = 11 / 4 = 2.75, which truncates to 2.

## Example

```javascript
Input: nums = [7,4,3,9,1,8,5,2,6], k = 3
Output: [-1,-1,-1,5,4,4,-1,-1,-1]
Explanation:
- avg[0], avg[1], and avg[2] are -1 because there are less than k elements before each index.
- The sum of the subarray centered at index 3 with radius 3 is: 7 + 4 + 3 + 9 + 1 + 8 + 5 = 37.
  Using integer division, avg[3] = 37 / 7 = 5.
- For the subarray centered at index 4, avg[4] = (4 + 3 + 9 + 1 + 8 + 5 + 2) / 7 = 4.
- For the subarray centered at index 5, avg[5] = (3 + 9 + 1 + 8 + 5 + 2 + 6) / 7 = 4.
- avg[6], avg[7], and avg[8] are -1 because there are less than k elements after each index.
```

## Solution

Great solution found [here](https://leetcode.com/problems/k-radius-subarray-averages/solutions/1599974/javascript-sliding-window/)

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var getAverages = function (nums, k) {
  //set up variables
  const twoK = 2 * k;
  const windowSize = twoK + 1;
  //create result array
  const result = [...nums].fill(-1);
  //create sum variable
  let sum = 0;
  //iterate through nums
  for (let i = 0; i < nums.length; i++) {
    //add nums[i] to sum
    sum += nums[i];
    //if i is greater than or equal to windowSize
    if (i >= twoK) {
      //set result[i - k] to sum / windowSize
      result[i - k] = Math.floor(sum / windowSize);
      //subtract nums[i - twoK] from sum
      sum -= nums[i - twoK];
    }
  }
  return result;
};
```
