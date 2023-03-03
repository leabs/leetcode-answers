---
layout: post
title: 28. Find the Index of the First Occurrence in a String
date: 2023-03-03 07:54 -0500
difficulty: medium
comments: true
---

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

## Example

```javascript
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
```

## Solution

```javascript
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function (haystack, needle) {
  //If needle is not within haystack, return -1
  if (!haystack.includes(needle)) {
    return -1;
  } else {
    //Return the index of the first occurrence of needle in haystack
    return haystack.indexOf(needle);
  }
};
```

