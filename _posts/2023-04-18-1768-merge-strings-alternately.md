---
layout: post
title: 1768. Merge Strings Alternately
date: 2023-04-18 08:08 -0400
difficulty: easy
comments: true
---

You are given two strings `word1` and `word2`. Merge the strings by adding letters in alternating order, starting with `word1`. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return the merged string.

## Example

```javascript
Input: word1 = "abc", word2 = "pqr"
Output: "apbqcr"
Explanation: The merged string will be merged as so:
word1:  a   b   c
word2:    p   q   r
merged: a p b q c r
```

## Solution

```javascript
/**
 * @param {string} word1
 * @param {string} word2
 * @return {string}
 */
var mergeAlternately = function (word1, word2) {
  //find the length of the longest string
  let longest = Math.max(word1.length, word2.length);
  //declare new array
  let newArr = [];
  //for loop to iterate through the longest string
  for (let i = 0; i < longest; i++) {
    //if word1[i] exists
    if (word1[i]) {
      //push word1[i] to new array
      newArr.push(word1[i]);
    }
    //if word2[i] exists
    if (word2[i]) {
      //push word2[i] to new array
      newArr.push(word2[i]);
    }
  }
  //return new array joined
  return newArr.join("");
};
```
