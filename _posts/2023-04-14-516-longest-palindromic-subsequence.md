---
layout: post
title: 516. Longest Palindromic Subsequence
date: 2023-04-14 09:28 -0400
difficulty: medium
comments: true
---

Given a string `s`, find the longest palindromic **subsequence's** length in `s`.

A **subsequence** is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

## Exmaple

```javascript
Input: s = "bbbab"
Output: 4
Explanation: One possible longest palindromic subsequence is "bbbb".
```

## Solution

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var longestPalindromeSubseq = function (s) {
  let n = s.length;
  // dp[i][j] is the longest palindromic subsequence's length of substring s[i..j]
  let dp = new Array(n).fill(0).map(() => new Array(n).fill(0));
  for (let i = n - 1; i >= 0; i--) {
    // Every single character is a palindrome of length 1
    dp[i][i] = 1;
    for (let j = i + 1; j < n; j++) {
      // If the two ends are the same, then the length is 2 plus the length of the remaining substring
      if (s[i] === s[j]) {
        // The two ends are included in the palindrome, so +2
        dp[i][j] = dp[i + 1][j - 1] + 2;
      }
      // Otherwise, the length is the maximum of the two substrings
      else {
        // The two ends are not included in the palindrome, so we take the maximum of the two substrings'
        dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
      }
    }
  }
  return dp[0][n - 1];
};
```
