---
layout: post
title: 1416. Restore The Array
date: 2023-04-23 08:19 -0400
difficulty: hard
comments: true
---

A program was supposed to print an array of integers. The program forgot to print whitespaces and the array is printed as a string of digits `s` and all we know is that all integers in the array were in the range `[1, k]` and there are no leading zeros in the array.

Given the string `s` and the integer `k`, return the number of the possible arrays that can be printed as s using the mentioned program. Since the answer may be very large, return it modulo 109 + 7.

## Example

```javascript
Input: s = "1000", k = 10000
Output: 1
Explanation: The only possible array is [1000]
```

## Solution

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {number}
 */
var numberOfArrays = function (s, k) {
  //Set mod to 10^9 + 7
  const mod = 10 ** 9 + 7;
  //Create an array to store the number of ways to print the string
  const dp = Array(s.length + 1).fill(0);
  //Set the first element to 1
  dp[0] = 1;
  //Loop through the string
  for (let i = 0; i < s.length; i++) {
    //If the first character is 0, then we can't print the string
    if (s[i] === "0") continue;
    //Create a variable to store the current number
    let num = 0;
    //Loop through the string
    for (let j = i; j < s.length; j++) {
      //Add the current character to the number
      num = num * 10 + Number(s[j]);
      //If the number is greater than k, then we can't print the string
      if (num > k) break;
      //Add the number of ways to print the string to the current index
      dp[j + 1] = (dp[j + 1] + dp[i]) % mod;
    }
  }
  //Return the number of ways to print the string
  return dp[s.length];
};
```
