---
layout: post
title: "452. Minimum Number of Arrows to Burst Balloons"
date: 2023-01-04 10:35:33 -0500
comments: true
difficulty: medium
---

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose horizontal diameter stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up directly vertically (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is burst by an arrow shot at `x` if `xstart <= x <= xend`. There is no limit to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return the minimum number of arrows that must be shot to burst all balloons.

```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var minimumRounds = function (tasks) {
  let counter = {},
    res = 0;
  //Count frequency of each task
  for (let t of tasks) {
    counter[t] = (counter[t] || 0) + 1;
  }
  //Go through the task and try to get 3(max) done each time.
  for (let k in counter) {
    //If the task only show up Once, that means not possible.
    if (counter[k] === 1) return -1;
    res += Math.ceil(counter[k] / 3);
  }
  return res;
};
```
