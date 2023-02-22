---
layout: post
title: 1523. Count Odd Numbers in an Interval Range
date: 2023-02-13 07:43 -0500
difficulty: easy
comments: true
---

Given two non-negative integers `low` and `high`. Return the count of _odd numbers between_ `low` and `high` _(inclusive)_.

## Example

```javascript
Input: low = 3, high = 7
Output: 3
Explanation: The odd numbers between 3 and 7 are [3,5,7].
```

## Solution

```javascript
/**
 * @param {number} l
 * @param {number} h
 * @return {number}
 */
var countOdds = function (l, h) {
  // If the lower bound is even, increment it
  return Math.floor((h + 1) / 2) - Math.floor(l / 2);
};
```
