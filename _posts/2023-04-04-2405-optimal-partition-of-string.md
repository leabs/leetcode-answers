---
layout: post
title: 2405. Optimal Partition of String
date: 2023-04-04 08:35 -0400
difficulty: medium
comments: true
---

Given a string `s`, partition the string into one or more substrings such that the characters in each substring are unique. That is, no letter appears in a single substring more than once.

Return the **minimum** number of substrings in such a partition.

Note that each character should belong to exactly one substring in a partition.

## Example

```javascript
Input: s = "abacaba"
Output: 4
Explanation:
Two possible partitions are ("a","ba","cab","a") and ("ab","a","ca","ba").
It can be shown that 4 is the minimum number of substrings needed.
```

## Solution

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var partitionString = function (s) {
  //Initialize counter
  let counter = 0;
  //Initialize set
  let set = new Set();
  //For s.length
  for (let i = 0; i < s.length; i++) {
    //If set has s[i]
    if (set.has(s[i])) {
      //Increment counter
      counter++;
      //Reset set
      set = new Set();
    }
    //Add s[i] to set
    set.add(s[i]);
  }
  //Return set size
  return set.size === 0 ? counter : counter + 1;
};
```
