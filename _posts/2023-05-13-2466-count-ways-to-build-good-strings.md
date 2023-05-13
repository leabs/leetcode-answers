---
layout: post
title: 2466. Count Ways To Build Good Strings
date: 2023-05-13 10:15 -0400
difficulty: medium
comments: true
---

Given the integers `zero`, `one`, `low`, and `high`, we can construct a string by starting with an empty string, and then at each step perform either of the following:

- Append the character `'0'` zero times.
- Append the character `'1'` one times.

This can be performed any number of times.

A good string is a string constructed by the above process having a length between `low` and `high` (**inclusive**).

Return the number of **different** _good strings that can be constructed satisfying these properties_. Since the answer can be large, return it modulo `109 + 7`.

## Example

```javascript
Input: low = 3, high = 3, zero = 1, one = 1
Output: 8
Explanation:
One possible valid good string is "011".
It can be constructed as follows: "" -> "0" -> "01" -> "011".
All binary strings from "000" to "111" are good strings in this example.
```

## Solution

Great solution [here](https://leetcode.com/problems/count-ways-to-build-good-strings/solutions/3517908/javascript-dp-simple-solution-with-comments/?languageTags=javascript)

```javascript
/**
 * @param {number} low
 * @param {number} high
 * @param {number} zero
 * @param {number} one
 * @return {number}
 */
var countGoodStrings = function (low, high, zero, one) {
  //Set mod
  const modulo = 1e9 + 7;
  let answ = 0;

  // dp array of lenght high + 1 filled with zeros
  // dp[i] denotes number of valid strings of lenght i
  const dp = Array(high + 1).fill(0);

  // an empty string "" can be constructed only in 1 way, so dp[0] = 1
  dp[0] = 1;

  for (let i = 1; i <= high; i++) {
    // for each i, a string of length i can be constructed
    // by adding either "0" zero time
    // or by adding "1" one times
    // dp[i] = dp[i - zero] + dp[i - one]

    if (i - zero >= 0) {
      dp[i] = (dp[i] + dp[i - zero]) % modulo;
    }
    if (i - one >= 0) {
      dp[i] = (dp[i] + dp[i - one]) % modulo;
    }

    // if i >= low start counting the total number of strings
    if (i >= low) {
      answ = (answ + dp[i]) % modulo;
    }
  }
  return answ;
};
```
