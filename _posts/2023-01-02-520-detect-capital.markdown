---
layout: post
title: "520. Detect Capital"
date: 2023-01-02 10:35:33 -0500
difficulty: easy
---

We define the usage of capitals in a word to be right when one of the following cases holds:

- All letters in this word are capitals, like `"USA"`.
- All letters in this word are not capitals, like `"leetcode"`.
- Only the first letter in this word is capital, like `"Google"`.

Given a string `word`, return `true` if the usage of capitals in it is right.

<pre><strong>Input:</strong> word = "USA"
<strong>Output:</strong> true
</pre>

## Solution

```javascript
/**
 * @param {string} word
 * @return {boolean}
 */
var detectCapitalUse = function (word) {
  //Case 1: All letters in this word are capitals, like "USA"
  if (word.toUpperCase() === word) return true;
  //Case 2: All letters in this word are not capitals, like "leetcode"
  if (word.toLowerCase() === word) return true;
  //Case 3: Only the first letter in this word is capital, like "Google"
  if (
    word[0].toUpperCase() === word[0] &&
    word.slice(1).toLowerCase() === word.slice(1)
  )
    return true;
  else {
    return false;
  }
};
```
