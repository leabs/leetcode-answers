---
layout: post
title: "57. Insert Interval"
date: 2023-01-16 07:35:33 -0500
comments: true
difficulty: medium
---

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

<pre><strong>Input:</strong> intervals = [[1,3],[6,9]], newInterval = [2,5]
<strong>Output:</strong> [[1,5],[6,9]]
</pre>

```javascript
/**
 * @param {number[][]} intervals
 * @param {number[]} newInterval
 * @return {number[][]}
 */

// O(n), O(n)
var insert = function (intervals, newInterval) {
  let [start, end] = newInterval;
  let left = [];
  let right = [];

  for (const interval of intervals) {
    const [first, last] = interval;

    // current interval is smaller than newInterval
    if (last < start) left.push(interval);
    // current interval is larger than newInterval
    else if (first > end) right.push(interval);
    // there is a overlap
    else {
      start = Math.min(start, first);
      end = Math.max(end, last);
    }
  }

  return [...left, [start, end], ...right];
};
```
