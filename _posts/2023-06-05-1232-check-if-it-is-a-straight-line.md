---
layout: post
title: 1232. Check If It Is a Straight Line
date: 2023-06-05 08:40 -0400
difficulty: easy
comments: true
---

You are given an array `coordinates`, `coordinates[i] = [x, y]`, where `[x, y]` represents the coordinate of a point. Check if these points make a straight line in the XY plane.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-5.jpg" alt="example line image" width="300"/>

```javascript
Input: coordinates = [
  [1, 2],
  [2, 3],
  [3, 4],
  [4, 5],
  [5, 6],
  [6, 7],
];
Output: true;
```

## Solution

```javascript
/**
 * @param {number[][]} coordinates
 * @return {boolean}
 */
var checkStraightLine = function (coordinates) {
  //Check to see if coordinates.length is 2
  if (coordinates.length === 2) {
    return true;
  }
  //Assign points to coordinates[0] and coordinates[1]
  let x1 = coordinates[0][0];
  let x2 = coordinates[1][0];
  let y1 = coordinates[0][1];
  let y2 = coordinates[1][1];

  if (x2 === x1) {
    for (let i = 2; i < coordinates.length; i++) {
      if (coordinates[i][0] !== x1) {
        return false;
      }
    }
    return true;
  }

  //Slope formula
  let slope = (y2 - y1) / (x2 - x1);

  //Loop through coordinates starting at index 2
  for (let i = 2; i < coordinates.length; i++) {
    let currentSlope =
      (coordinates[i][1] - coordinates[i - 1][1]) /
      (coordinates[i][0] - coordinates[i - 1][0]);
    if (slope !== currentSlope) {
      return false;
    }
  }
  return true;
};
```
