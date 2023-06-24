---
layout: post
title: 956. Tallest Billboard
date: 2023-06-24 08:32 -0400
difficulty: hard
comments: true
---

You are installing a billboard and want it to have the largest height. The billboard will have two steel supports, one on each side. Each steel support must be an equal height.

You are given a collection of rods that can be welded together. For example, if you have rods of lengths 1, 2, and 3, you can weld them together to make a support of length 6.

Return the largest possible height of your billboard installation. If you cannot support the billboard, return 0.

## Example

```javascript
Input: rods = [1,2,3,6]
Output: 6
Explanation: We have two disjoint subsets {1,2,3} and {6}, which have the same sum = 6.
```

## Solution

Great solution found [here](https://leetcode.com/problems/tallest-billboard/solutions/990915/javascript-solution-dp/)

```javascript
/**
 * @param {number[]} rods
 * @return {number}
 */
var tallestBillboard = function(rods) {
    let len = rods.length;
    if (len <= 1) return 0;
    let dp = [];
    for (let i = 0; i < len + 5; i++) {
        dp[i] = [];
        for (let j = 0; j < 5005 * 2; j++) {
            dp[i][j] = -1
        }
    }
    return solve(0, 0, rods, dp);
}

var solve = function(i, sum, rods, dp) {
    // If we have reached the end of the array, we need to return the correct value
    if (i == rods.length) {
        // If the sum is 0, then we know that the two piles are the same height
        if (sum == 0) {
            // We return 0 because we don't need to add any more to the piles
            return 0
        }else{
            // If the sum is not 0, then we return a very large negative number
            // because it is not possible to have two piles with the same height
            return -5000
        }
    }
    // If we have already calculated the value for this state, then we return it
    if (dp[i][sum + 5000] != -1) {
        return dp[i][sum + 5000];
    }
    // We can either add the current value to the left pile, the right pile, or not add it at all
    let val = solve(i + 1, sum, rods, dp);
    val = Math.max(val, solve(i + 1, sum + rods[i], rods, dp) + rods[i]);
    val = Math.max(val, solve(i + 1, sum - rods[i], rods, dp));
    // We save the value for this state so that we don't have to calculate it again
    dp[i][sum + 5000] = val;
    return val;
}
```
