---
layout: post
title: 1456. Maximum Number of Vowels in a Substring of Given Length
date: 2023-05-05 08:53 -0400
difficulty: medium
comments: true
---

Given a string `s` and an integer `k`, return the _maximum number of vowel letters in any substring of `s` with length `k`_.

**Vowel letters** in English are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`.

## Example

```javascript
Input: s = "abciiidef", k = 3
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.
```

## Solution

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {number}
 */
var maxVowels = function (s, k) {
  //Given a string s and an integer k, return the maximum number of vowel letters in any substring of s with length k.
  let vowels = ["a", "e", "i", "o", "u"];
  let max = 0;
  let count = 0;
  //Loop through the string
  for (let i = 0; i < s.length; i++) {
    //If the current character is a vowel, increment the count
    if (vowels.includes(s[i])) {
      count++;
    }
    //If the current index is greater than k, decrement the count if the character at the index k - 1 is a vowel
    if (i >= k && vowels.includes(s[i - k])) {
      count--;
    }
    //Set the max to the max of the current max and the count
    max = Math.max(max, count);
  }
  return max;
};
```
