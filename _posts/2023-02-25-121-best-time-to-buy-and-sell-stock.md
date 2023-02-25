---
layout: post
title: 121. Best Time to Buy and Sell Stock
date: 2023-02-25 09:24 -0500
difficulty: easy
comments: true
---

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

## Example

```javascript
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

## Solution

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  //Set profit to 0
  let profit = 0;
  //Set min to prices[0]
  let min = prices[0];
  for (let i = 1; i < prices.length; i++) {
    //The day we should buy at
    min = Math.min(min, prices[i - 1]);
    //Check if selling at the current day gives us the most profit
    profit = Math.max(prices[i] - min, profit);
  }
  return profit;
};
```
