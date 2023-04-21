---
layout: post
title: 879. Profitable Schemes
date: 2023-04-21 08:02 -0400
difficulty: hard
comments: true
---

There is a group of `n` members, and a list of various crimes they could commit. The `ith` crime generates a `profit[i]` and requires `group[i]` members to participate in it. If a member participates in one crime, that member can't participate in another crime.

Let's call a profitable scheme any subset of these crimes that generates at least `minProfit` profit, and the total number of members participating in that subset of crimes is at most `n`.

Return the number of schemes that can be chosen. Since the answer may be very large, return it modulo `109 + 7`.

## Example

```javascript
Input: n = 5, minProfit = 3, group = [2,2], profit = [2,3]
Output: 2
Explanation: To make a profit of at least 3, the group could either commit crimes 0 and 1, or just crime 1.
In total, there are 2 schemes.
```

## Solution

Great solution found [here](https://leetcode.com/problems/profitable-schemes/solutions/3439639/3d-dp-python-js-solution-explained/?orderBy=most_votes&languageTags=javascript).

```javascript
/**
 * @param {number} n
 * @param {number} minProfit
 * @param {number[]} group
 * @param {number[]} profit
 * @return {number}
 */
var profitableSchemes = function (n, minProfit, group, profit) {
  const gLen = group.length;
  // dp[i][j][k] means the number of schemes with i crimes, j members, and k profit
  const dp = Array(gLen + 1)
    .fill()
    .map(() => {
      return Array(n + 1)
        .fill()
        .map(() => Array(minProfit + 1).fill(0));
    });

  //base case
  dp[0][0][0] = 1;

  const mod = 10 ** 9 + 7;

  let result = 0;
  // for each crime
  for (let i = 1; i <= gLen; i++) {
    for (let j = 0; j <= n; j++) {
      for (let k = 0; k <= minProfit; k++) {
        if (j < group[i - 1]) dp[i][j][k] = dp[i - 1][j][k];
        else
          dp[i][j][k] =
            (dp[i - 1][j][k] +
              dp[i - 1][j - group[i - 1]][Math.max(0, k - profit[i - 1])]) %
            mod;
      }
    }
  }
  // sum up all the schemes that have at least minProfit
  for (let i = 0; i <= n; i++) {
    result = (result + dp[gLen][i][minProfit]) % mod;
  }

  return result;
};
```
