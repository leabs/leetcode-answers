---
layout: post
title: "452. Minimum Number of Arrows to Burst Balloons"
date: 2023-01-05 07:35:33 -0500
comments: true
difficulty: medium
---

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose **horizontal diameter** stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up directly vertically (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is burst by an arrow shot at `x` if `xstart <= x <= xend`. There is no limit to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return the minimum number of arrows that must be shot to burst all balloons.

<pre><strong>Input:</strong> points = [[10,16],[2,8],[1,6],[7,12]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].
</pre>

```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var findMinArrowShots = function (points) {
  // if the very left edge of the balloons are sorted (min to max)
  // then we only need to track the overlap and right edges
  points.sort((a, b) => a[0] - b[0]);

  // if there is at least one balloon
  // then a minimum of one dart is required

  let darts = 1;
  let currentOverlapR = points[0][1]; // right edge of previous overlap

  for (let i = 1; i < points.length; i++) {
    // if the current balloon's left edge is greater than the right
    // edge of our current overlap, so we need another dart
    if (points[i][0] > currentOverlapR) {
      darts++;
      currentOverlapR = points[i][1]; // reset the overlapping edge
      continue;
    }
    if (points[i][1] <= currentOverlapR) {
      // don't need to increment darts here due to overlap
      // but we do need to adjust where the right edge ends
      currentOverlapR = Math.min(currentOverlapR, points[i][1]);
    }
  }

  return darts;
};
```
