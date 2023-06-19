---
layout: post
title: 1732. Find the Highest Altitude
date: 2023-06-19 08:14 -0400
difficulty: easy
comments: true
---

There is a biker going on a road trip. The road trip consists of n + 1 points at different altitudes. The biker starts his trip on point 0 with altitude equal 0.

You are given an integer array gain of length n where gain[i] is the net gain in altitude between points i​​​​​​ and i + 1 for all (0 <= i < n). Return the highest altitude of a point.

## Example

```javascript
Input: gain = [-5,1,5,0,-7]
Output: 1
Explanation: The altitudes are [0,-5,-4,1,1,-6]. The highest is 1.
```

## Solution

```javascript
/**
 * @param {number[]} gain
 * @return {number}
 */
var largestAltitude = function (gain) {
  // Set max to 0
  let max = 0;
  // Set current to 0
  let current = 0;
  // Iterate through gain
  for (let i = 0; i < gain.length; i++) {
    // Add gain[i] to current
    current += gain[i];
    // If current is greater than max
    if (current > max) {
      // Set max to current
      max = current;
    }
  }
  // Return max
  return max;
};
```
