---
layout: post
title: "926. Flip String to Monotone Increasing"
date: 2023-01-17 07:35:33 -0500
comments: true
difficulty: medium
---

A binary string is monotone increasing if it consists of some number of `0`'s (possibly none), followed by some number of `1`'s (also possibly none).

You are given a binary string `s`. You can flip `s[i]` changing it from `0` to `1` or from `1` to `0`.

Return the minimum number of flips to make `s` monotone increasing.

<pre><strong>Input:</strong> s = "00110"
<strong>Output:</strong> 1
<strong>Explanation:</strong> We flip the last digit to get 00111.
</pre>

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var minFlipsMonoIncr = function (s) {
  // count the number of 1's
  let ones = 0;
  // count the number of flips
  let flips = 0;
  // loop through the string
  for (let i = 0; i < s.length; i++) {
    // if the current character is 1
    if (s[i] === "1") {
      ones++;
    } else {
      flips++;
    }
    // if the number of flips is less than the number of 1's
    flips = Math.min(flips, ones);
  }
  // return the number of flips
  return flips;
};
```
