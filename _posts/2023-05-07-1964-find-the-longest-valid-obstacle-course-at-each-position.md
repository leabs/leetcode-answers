---
layout: post
title: 1964. Find the Longest Valid Obstacle Course at Each Position
date: 2023-05-07 09:42 -0400
difficulty: hard
comments: true
---

You want to build some obstacle courses. You are given a 0-indexed integer array `obstacles` of length `n`, where `obstacles[i]` describes the height of the `ith` obstacle.

For every index `i` between `0` and `n - 1` **(inclusive)**, find the length of the **longest obstacle course** in `obstacles` such that:

- You choose any number of obstacles between `0` and `i` inclusive.
- You must include the `ith` obstacle in the course.
- You must put the chosen obstacles in the same order as they appear in `obstacles`.
- Every obstacle (except the first) is taller than or the same height as the obstacle immediately before it.

Return an array `ans` of length `n`, where `ans[i]` is the length of the longest obstacle course for index `i` as described above.

## Example

```javascript
Input: obstacles = [1,2,3,2]
Output: [1,2,3,3]
Explanation: The longest valid obstacle course at each position is:
- i = 0: [1], [1] has length 1.
- i = 1: [1,2], [1,2] has length 2.
- i = 2: [1,2,3], [1,2,3] has length 3.
- i = 3: [1,2,3,2], [1,2,2] has length 3.
```

## Solution

Great solution found [here](https://leetcode.com/problems/find-the-longest-valid-obstacle-course-at-each-position/solutions/1390411/javascript-lis-and-binary-search-upperbound/?orderBy=most_votes&languageTags=javascript)

```javascript
/**
 * @param {number[]} obstacles
 * @return {number[]}
 */
var longestObstacleCourseAtEachPosition = function (obstacles) {
  // Decalere obstacles length, lis array, and res array
  var n = obstacles.length;
  var lis = [];
  var res = new Array(n).fill(0);
  for (var i = 0; i < n; i++) {
    // if the lis is empty or the current obstacle is greater than the last element of lis
    if (lis.length > 0 && obstacles[i] >= lis[lis.length - 1]) {
      // push the current obstacle to lis
      lis.push(obstacles[i]);
      // set res[i] to lis length
      res[i] = lis.length;
    } else {
      // find the upper bound
      var l = 0;
      var r = lis.length;
      while (l <= r) {
        // set mid to the floor of the average of l and r
        var mid = Math.floor((l + r) / 2);
        // if the mid element of lis is less than or equal to the current obstacle
        if (lis[mid] <= obstacles[i]) {
          l = mid + 1;
        } else {
          r = mid - 1;
        }
      }
      // set lis[l] to the current obstacle
      lis[l] = obstacles[i];
      // set res[i] to l+1
      res[i] = l + 1;
    }
  }
  return res;
};
```
