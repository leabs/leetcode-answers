---
layout: post
title: 1312. Minimum Insertion Steps to Make a String Palindrome
date: 2023-04-22 08:38 -0400
difficulty: hard
comments: true
---

Given a string `s`. In one step you can insert any character at any index of the string.

Return the minimum number of steps to make `s` palindrome.

A Palindrome String is one that reads the same backward as well as forward.

## Example

```javascript
Input: s = "zzazz"
Output: 0
Explanation: The string "zzazz" is already palindrome we do not need any insertions.
```

## Solution

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var minInsertions = function (s) {
  //Check if the string is already a palindrome
  if (s === s.split("").reverse().join("")) return 0;

  //Create a 2D array to store the number of insertions needed to make a string palindrome
  const dp = Array(s.length)
    .fill()
    .map(() => Array(s.length).fill(0));

  //Loop through the string
  for (let i = s.length - 1; i >= 0; i--) {
    for (let j = i + 1; j < s.length; j++) {
      //If the characters at i and j are the same, then we don't need to insert anything
      if (s[i] === s[j]) dp[i][j] = dp[i + 1][j - 1];
      //If the characters at i and j are not the same, then we need to insert the character at i or j
      else dp[i][j] = Math.min(dp[i + 1][j], dp[i][j - 1]) + 1;
    }
  }

  return dp[0][s.length - 1];
};
```
