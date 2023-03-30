---
layout: post
title: 87. Scramble String
date: 2023-03-30 09:19 -0400
difficulty: hard
comments: true
---

We can scramble a string s to get a string t using the following algorithm:

If the length of the string is 1, stop.

If the length of the string is > 1, do the following:

- Split the string into two non-empty substrings at a random index, i.e., if the string is s, divide it to `x` and `y` where `s = x + y`.
- Randomly decide to swap the two substrings or to keep them in the same order. i.e., after this step, `s` may become `s = x + y` or `s = y + x`.
- Apply step 1 recursively on each of the two substrings `x` and `y`.

Given two strings `s1` and `s2` of the same length, return `true` if `s2` is a scrambled string of `s1`, otherwise, return `false`.

## Example

```javascript
Input: s1 = "great", s2 = "rgeat"
Output: true
Explanation: One possible scenario applied on s1 is:
"great" --> "gr/eat" // divide at random index.
"gr/eat" --> "gr/eat" // random decision is not to swap the two substrings and keep them in order.
"gr/eat" --> "g/r / e/at" // apply the same algorithm recursively on both substrings. divide at random index each of them.
"g/r / e/at" --> "r/g / e/at" // random decision was to swap the first substring and to keep the second substring in the same order.
"r/g / e/at" --> "r/g / e/ a/t" // again apply the algorithm recursively, divide "at" to "a/t".
"r/g / e/ a/t" --> "r/g / e/ a/t" // random decision is to keep both substrings in the same order.
The algorithm stops now, and the result string is "rgeat" which is s2.
As one possible scenario led s1 to be scrambled to s2, we return true.
```

## Solution

Great solution found [here](https://leetcode.com/problems/scramble-string/solutions/1277442/javascript-easy-explained-solution/?orderBy=most_votes&languageTags=javascript)

```javascript
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var isScramble = function (s1, s2) {
  let cache = {};

  return match(s1, s2);

  function match(s1, s2) {
    let res = false;
    if (cache[s1 + s2] !== undefined) {
      return cache[s1 + s2];
    }
    if (cache[s2 + s1] !== undefined) {
      return cache[s2 + s1];
    }
    if (s1.length === 1) {
      return s1 === s2;
    }
    let s1FirstPart, s1SecondPart, s2FirstPart, s2SecondPart;
    for (let i = 0; i < s1.length - 1; i++) {
      //first i+1 chars
      s1FirstPart = s1.substring(0, i + 1);
      //rest of the chars
      s1SecondPart = s1.substring(i + 1);
      //first i+1 chars
      s2FirstPart = s2.substring(0, i + 1);
      //rest of the chars
      s2SecondPart = s2.substring(i + 1);
      if (
        match(s1FirstPart, s2FirstPart) &&
        match(s1SecondPart, s2SecondPart)
      ) {
        res = true;
        break;
      }
      //last i+1 chars
      s2FirstPart = s2.substring(s2.length - 1 - i);
      //rest of the chars
      s2SecondPart = s2.substring(0, s2.length - 1 - i);
      if (
        match(s1FirstPart, s2FirstPart) &&
        match(s1SecondPart, s2SecondPart)
      ) {
        res = true;
        break;
      }
    }
    cache[s1 + s2] = res;
    cache[s2 + s1] = res;
    return res;
  }
};
```
