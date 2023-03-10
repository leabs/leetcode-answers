---
layout: post
title: "131. Palindrome Partitioning"
date: 2023-01-22 10:07 -0500
difficulty: medium
comments: true
---

Given a string `s`, partition `s` such that every substring of the partition is a palindrome. Return _all possible palindrome partitioning of_ `s`.

<pre><strong>Input:</strong> s = "aab"
<strong>Output:</strong> [["a","a","b"],["aa","b"]]
</pre>

## Solution

```javascript
/**
 * @param {string} s
 * @return {string[][]}
 */
var partition = function (s) {
  //Declare empty results array
  let result = [];

  //Declare helper function to find all possible palindromes
  findP(0, []);
  //Return results
  return result;

  //Helper function to find all possible palindromes
  function findP(start, arr) {
    //If start is equal to the length of the string, push the array into the results array
    if (start === s.length) {
      result.push(arr.slice());
      return;
    }
    //Loop through the string
    for (let i = start; i < s.length; i++) {
      //Declare a variable to hold the substring
      let str = s.slice(start, i + 1);
      //If the substring is a palindrome, call the helper function again
      if (isPalindrom(str)) {
        findP(i + 1, [...arr, str]);
      }
    }
  }
  //Helper function to check if a string is a palindrome
  function isPalindrom(str) {
    //Loop through the string
    for (let i = 0; i < str.length / 2; i++) {
      //If the character at the current index is not equal to the character at the current index from the end of the string, return false
      if (str[i] !== str[str.length - 1 - i]) return false;
    }
    return true;
  }
};
```
