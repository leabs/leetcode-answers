---
layout: post
title: 2439. Minimize Maximum of Array
date: 2023-04-05 08:04 -0400
difficulty: medium
comments: true
---

You are given a 0-indexed array `nums` comprising of `n` non-negative integers.

In one operation, you must:

- Choose an integer `i` such that `1 <= i < n` and `nums[i] > 0`.
- Decrease `nums[i]` by 1.
- Increase `nums[i - 1]` by 1.

Return the minimum possible value of the maximum integer of `nums` after performing any number of operations.

## Example

```javascript
Input: nums = [3,7,1,6]
Output: 5
Explanation:
One set of optimal operations is as follows:
1. Choose i = 1, and nums becomes [4,6,1,6].
2. Choose i = 3, and nums becomes [4,6,2,5].
3. Choose i = 1, and nums becomes [5,5,2,5].
The maximum integer of nums is 5. It can be shown that the maximum number cannot be less than 5.
Therefore, we return 5.
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var minimizeArrayValue = function (nums) {
  //Initialize res and total
  let res = nums[0],
    total = nums[0];
  for (let i = 1; i < nums.length; i++) {
    //total is the sum of all elements in nums
    total += nums[i];
    //res is the maximum of res and the ceiling of total/(i+1)
    res = Math.max(res, Math.ceil(total / (i + 1)));
  }
  return res;
};
```
