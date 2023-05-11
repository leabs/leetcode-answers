---
layout: post
title: 1035. Uncrossed Lines
date: 2023-05-11 07:54 -0400
difficulty: medium
comments: true
---

You are given two integer arrays `nums1` and `nums2`. We write the integers of `nums1` and `nums2` (in the order they are given) on two separate horizontal lines.

We may draw connecting lines: a straight line connecting two numbers `nums1[i]` and `nums2[j]` such that:

- `nums1[i] == nums2[j]`, and
- the line we draw does not intersect any other connecting (non-horizontal) line.

Note that a connecting line cannot intersect even at the endpoints (i.e., each number can only belong to one connecting line).

Return the _maximum number of connecting lines we can draw in this way_.

## Example

<img src="{{ site.baseurl }}/assets/images/may-11.png" alt="Example grid image"  style="max-width:300px" />

```javascript
Input: nums1 = [1,4,2], nums2 = [1,2,4]
Output: 2
Explanation: We can draw 2 uncrossed lines as in the diagram.
We cannot draw 3 uncrossed lines, because the line from nums1[1] = 4 to nums2[2] = 4 will intersect the line from nums1[2]=2 to nums2[1]=2.
```

## Solution

Great solution found [here](https://leetcode.com/problems/uncrossed-lines/solutions/1566234/javascript-dp-solution-with-space-optimization-beats-100/?orderBy=most_votes&languageTags=javascript).

```javascript
var maxUncrossedLines = function (nums1, nums2) {
  //Set m to nums1 length and n to nums2 length
  const m = nums1.length,
    n = nums2.length;

  //If m is less than n, return maxUncrossedLines(nums2, nums1)
  if (m < n) return maxUncrossedLines(nums2, nums1);

  //Set previous and current to arrays of length n + 1 filled with 0s
  let previous = Array(n + 1).fill(0);
  let current = Array(n + 1).fill(0);

  //For each number in nums1
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      //If the number in nums1 is equal to the number in nums2
      if (nums1[i - 1] == nums2[j - 1]) {
        //Set current[j] to 1 + previous[j - 1]
        current[j] = 1 + previous[j - 1];
      } else {
        //Set current[j] to the max of previous[j] and current[j - 1]
        current[j] = Math.max(previous[j], current[j - 1]);
      }
    }
    //Set previous to current and current to previous
    [previous, current] = [current, previous];
  }
  //Return previous[n]
  return previous[n];
};
```
