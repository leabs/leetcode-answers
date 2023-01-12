---
layout: post
title: "452. Minimum Number of Arrows to Burst Balloons"
date: 2023-01-04 10:35:33 -0500
published: false
---

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose horizontal diameter stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up directly vertically (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is burst by an arrow shot at `x` if `xstart <= x <= xend`. There is no limit to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return the minimum number of arrows that must be shot to burst all balloons.

```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var findMinArrowShots = function (points) {
  //set arrows to 0
  let arrows = 0;

  //sort points by x axis

  //FOR loop to calc # of arrows
  for (i = 0; points[0].length; i++) {
    //if points[i] == arrow. arrows++
    if (points[i]) {
      arrows++;
    }
  }
  return arrows;
};
```
