---
layout: post
title: 2187. Minimum Time to Complete Trips
date: 2023-03-07 08:03 -0500
difficulty: medium
comments: true
---

You are given an array `time` where `time[i]` denotes the time taken by the `ith` bus to complete **one trip**.

Each bus can make multiple trips **successively**; that is, the next trip can start **immediately after** completing the current trip. Also, each bus operates **independently**; that is, the trips of one bus do not influence the trips of any other bus.

You are also given an integer `totalTrips`, which denotes the number of trips all buses should make in total. Return the minimum time required for all buses to complete **at least** `totalTrips` trips.

## Example

```javascript
Input: time = [1,2,3], totalTrips = 5
Output: 3
Explanation:
- At time t = 1, the number of trips completed by each bus are [1,0,0].
  The total number of trips completed is 1 + 0 + 0 = 1.
- At time t = 2, the number of trips completed by each bus are [2,1,0].
  The total number of trips completed is 2 + 1 + 0 = 3.
- At time t = 3, the number of trips completed by each bus are [3,1,1].
  The total number of trips completed is 3 + 1 + 1 = 5.
So the minimum time needed for all buses to complete at least 5 trips is 3.
```

## Solution

Great solution [here](https://leetcode.com/problems/minimum-time-to-complete-trips/solutions/1802834/javascript-100-faster-easy-clean-code/?orderBy=hot&languageTags=javascript).

```javascript
/**
 * @param {number[]} time
 * @param {number} totalTrips
 * @return {number}
 */
var minimumTime = function (time, totalTrips) {
  let low = 1;
  let high = Number.MAX_SAFE_INTEGER;
  let ans = 0;

  while (low <= high) {
    // find the mid to prevent overflow
    let mid = Math.floor(low + (high - low) / 2);
    // check if it is possible to complete the trips in the given time
    if (isPossible(time, mid, totalTrips)) {
      ans = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }
  return ans;
};
// Check if it is possible to complete the trips in the given time
function isPossible(arr, mid, totalTrips) {
  let trips = 0;
  for (let i = 0; i < arr.length; i++) {
    // find the number of trips completed by each bus
    trips += Math.floor(mid / arr[i]);
  }
  return trips >= totalTrips;
}
```
