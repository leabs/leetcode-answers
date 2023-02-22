---
layout: post
title: 1011. Capacity To Ship Packages Within D Days
date: 2023-02-22 00:29 -0500
difficulty: medium
comments: true
---

A conveyor belt has packages that must be shipped from one port to another within `days` days.

The `ith` package on the conveyor belt has a weight of `weights[i]`. Each day, we load the ship with packages on the conveyor belt (in the order given by `weights`). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `days` days.

## Example

```javascript
Input: weights = [1,2,3,4,5,6,7,8,9,10], days = 5
Output: 15
Explanation: A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.
```

## Solution

```javascript
/**
 * @param {number[]} weights
 * @param {number} days
 * @return {number}
 */
var shipWithinDays = function (weights, days) {
  //Identify the minimum and maximum weights.
  let min = Math.max(...weights);
  let max = weights.reduce((a, b) => a + b);
  //Loop through the weights to identify the minimum weight capacity.
  while (min < max) {
    //Identify the middle weight capacity.
    let mid = Math.floor((min + max) / 2);
    //Identify the number of days it will take to ship the packages.
    let daysNeeded = 1;
    let currentWeight = 0;
    for (let i = 0; i < weights.length; i++) {
      //If the current weight plus the next weight is greater than the middle weight capacity, increment the number of days needed.
      if (currentWeight + weights[i] > mid) {
        daysNeeded++;
        currentWeight = 0;
      }
      //Add the next weight to the current weight.
      currentWeight += weights[i];
    }
    //If the number of days needed is greater than the number of days, increment the minimum weight capacity.
    if (daysNeeded > days) {
      min = mid + 1;
    } else {
      //If the number of days needed is less than or equal to the number of days, decrement the maximum weight capacity.
      max = mid;
    }
  }
  return min;
};
```
