---
layout: post
title: 1502. Can Make Arithmetic Progression From Sequence
date: 2023-06-06 07:53 -0400
difficulty: easy
comments: true
---

A sequence of numbers is called an **arithmetic progression** if the difference between any two consecutive elements is the same.

Given an array of numbers `arr`, return `true` if the array can be rearranged to form an arithmetic progression. Otherwise, return `false`.

## Example

```javascript
Input: arr = [3,5,1]
Output: true
Explanation: We can reorder the elements as [1,3,5] or [5,3,1] with differences 2 and -2 respectively, between each consecutive elements.
```

## Solution

```javascript
var canMakeArithmeticProgression = function (arr) {
  // sort the array
  arr.sort((a, b) => a - b);
  // find the difference between the first two elements
  let diff = arr[1] - arr[0];
  // iterate through the array and check if the difference between any two consecutive elements is the same
  for (let i = 1; i < arr.length; i++) {
    // if not, return false
    if (arr[i] - arr[i - 1] !== diff) {
      return false;
    }
  }
  return true;
};
```
