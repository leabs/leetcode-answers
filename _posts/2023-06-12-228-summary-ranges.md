---
layout: post
title: 228. Summary Ranges
date: 2023-06-12 08:02 -0400
difficulty: easy
comments: true
---

You are given a sorted unique integer array `nums`.

A range `[a,b]` is the set of all integers from `a` to `b` (inclusive).

Return the smallest sorted list of ranges that cover all the numbers in the array exactly. That is, each element of `nums` is covered by exactly one of the ranges, and there is no integer `x` such that `x` is in one of the ranges but not in `nums`.

Each range `[a,b]` in the list should be output as:

- `"a->b"` if `a != b`
- `"a"` if `a == b`

## Example

```javascript
Input: nums = [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: The ranges are:
[0,2] --> "0->2"
[4,5] --> "4->5"
[7,7] --> "7"
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function (nums) {
  for (let i = 0; i < nums.length; i++) {
    let j = i;
    // find the end of the range
    while (nums[j] + 1 === nums[j + 1]) j++;
    // if the range is more than one number, replace the range with the start and end
    if (j > i) {
      nums[i] = nums[i] + "->" + nums[j];
      nums.splice(i + 1, j - i);
    }
    // if the range is one number, just convert it to a string
    if (j === i) nums[i] = nums[i] + "";
  }
  return nums;
};
```
