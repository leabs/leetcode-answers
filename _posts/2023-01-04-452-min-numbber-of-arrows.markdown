---
layout: post
title: "2244. Minimum Rounds to Complete All Tasks"
date: 2023-01-04 10:35:33 -0500
comments: true
difficulty: medium
---

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose horizontal diameter stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up directly vertically (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is burst by an arrow shot at `x` if `xstart <= x <= xend`. There is no limit to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return the minimum number of arrows that must be shot to burst all balloons.

<pre><strong>Input:</strong> tasks = [2,2,3,3,2,4,4,4,4,4]
<strong>Output:</strong> 4
<strong>Explanation:</strong> To complete all the tasks, a possible plan is:
- In the first round, you complete 3 tasks of difficulty level 2. 
- In the second round, you complete 2 tasks of difficulty level 3. 
- In the third round, you complete 3 tasks of difficulty level 4. 
- In the fourth round, you complete 2 tasks of difficulty level 4.  
It can be shown that all the tasks cannot be completed in fewer than 4 rounds, so the answer is 4.
</pre>

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
