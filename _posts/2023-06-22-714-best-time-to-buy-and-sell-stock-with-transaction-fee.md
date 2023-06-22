---
layout: post
title: 714. Best Time to Buy and Sell Stock with Transaction Fee
date: 2023-06-22 08:06 -0400
difficulty: medium
comments: true
---

You are given an array prices where prices[i] is the price of a given stock on the ith day, and an integer fee representing a transaction fee.

Find the maximum profit you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

## Example

```javascript
Input: prices = [1,3,2,8,4,9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
- Buying at prices[0] = 1
- Selling at prices[3] = 8
- Buying at prices[4] = 4
- Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

## Solution

```javascript
/**
 * @param {number[]} prices
 * @param {number} fee
 * @return {number}
 */
var maxProfit = function (prices, fee) {
  // Set max to 0
  let max = 0;
  // Set min to prices[0]
  let min = prices[0];
  // Iterate through prices
  for (let i = 1; i < prices.length; i++) {
    // If prices[i] is less than min
    if (prices[i] < min) {
      // Set min to prices[i]
      min = prices[i];
    }
    // If prices[i] is greater than min plus fee
    if (prices[i] > min + fee) {
      // Set max to max plus prices[i] minus min minus fee
      max += prices[i] - min - fee;
      // Set min to prices[i] minus fee
      min = prices[i] - fee;
    }
  }
  // Return max
  return max;
};
```
