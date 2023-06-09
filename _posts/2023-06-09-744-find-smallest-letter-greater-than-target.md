---
layout: post
title: 744. Find Smallest Letter Greater Than Target
date: 2023-06-09 07:52 -0400
difficulty: easy
comments: true
---

You are given an array of characters `letters` that is sorted in non-decreasing order, and a character `target`. There are at least two different characters in `letters`.

Return the smallest character in `letters` that is lexicographically greater than target. If such a character does not exist, return the first character in `letters`.

## Example

```javascript
Input: letters = ["c","f","j"], target = "a"
Output: "c"
Explanation: The smallest character that is lexicographically greater than 'a' in letters is 'c'.
```

## Solution

```javascript
/**
 * @param {character[]} letters
 * @param {character} target
 * @return {character}
 */
var nextGreatestLetter = function (letters, target) {
  //return the smallest character in letters that is lexicographically greater than target
  //if target is greater than or equal to the last character in letters, return the first character in letters
  if (target >= letters[letters.length - 1]) return letters[0];
  for (let i = 0; i < letters.length; i++) {
    if (letters[i] > target) {
      return letters[i];
    }
  }
};
```
