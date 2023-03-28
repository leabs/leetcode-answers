---
layout: post
title: 983. Minimum Cost For Tickets
date: 2023-03-28 08:42 -0400
difficulty: medium
comments: true
---

You have planned some train traveling one year in advance. The days of the year in which you will travel are given as an integer array `days`. Each day is an integer from `1` to `365`.

Train tickets are sold in three different ways:

- a 1-day pass is sold for `costs[0]` dollars,
- a 7-day pass is sold for `costs[1]` dollars, and
- a 30-day pass is sold for `costs[2]` dollars.

The passes allow that many days of consecutive travel.

- For example, if we get a 7-day pass on day `2`, then we can travel for `7` days: `2`, `3`, `4`, `5`, `6`, `7`, and `8`.

Return the minimum number of dollars you need to travel every day in the given list of days.

## Example

```javascript
Input: days = [1,4,6,7,8,20], costs = [2,7,15]
Output: 11
Explanation: For example, here is one way to buy passes that lets you travel your travel plan:
On day 1, you bought a 1-day pass for costs[0] = $2, which covered day 1.
On day 3, you bought a 7-day pass for costs[1] = $7, which covered days 3, 4, ..., 9.
On day 20, you bought a 1-day pass for costs[0] = $2, which covered day 20.
In total, you spent $11 and covered all the days of your travel.
```

## Solution

```javascript
/**
 * @param {number[]} days
 * @param {number[]} costs
 * @return {number}
 */
var mincostTickets = function (days, costs) {
  //Array to store the minimum cost for each day
  let dp = new Array(366).fill(0);

  // Set of days where we need to travel
  let travelDays = new Set(days);

  for (let i = 1; i < dp.length; i++) {
    //If we don't need to travel on this day, the cost is the same as the previous day
    if (!travelDays.has(i)) {
      dp[i] = dp[i - 1];
    } else {
      //Otherwise, the cost is the minimum of the cost of the previous day, the cost of 7 days ago, or the cost of 30 days ago
      dp[i] = Math.min(
        dp[i - 1] + costs[0],
        dp[Math.max(0, i - 7)] + costs[1],
        dp[Math.max(0, i - 30)] + costs[2]
      );
    }
  }
  //Return the cost for the last day
  return dp[dp.length - 1];
};
```
