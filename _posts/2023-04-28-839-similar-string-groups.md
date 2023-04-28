---
layout: post
title: 839. Similar String Groups
date: 2023-04-28 08:32 -0400
difficulty: hard
comments: true
---

Two strings `X` and `Y` are similar if we can swap two letters (in different positions) of `X`, so that it equals `Y`. Also two strings `X` and `Y` are similar if they are equal.

For example, `"tars"` and `"rats"` are similar (swapping at positions `0` and `2`), and `"rats"` and `"arts"` are similar, but `"star"` is not similar to `"tars"`, `"rats"`, or `"arts"`.

Together, these form two connected groups by similarity: `{"tars", "rats", "arts"}` and `{"star"}`. Notice that `"tars"` and `"arts"` are in the same group even though they are not similar. Formally, each group is such that a word is in the group if and only if it is similar to at least one other word in the group.

We are given a list `strs` of strings where every string in `strs` is an anagram of every other string in `strs`. How many groups are there?

## Example

```javascript
Input: strs = ["tars", "rats", "arts", "star"];
Output: 2;
```

## Solution

```javascript
/**
 * @param {string[]} strs
 * @return {number}
 */
var numSimilarGroups = function (strs) {
  // set l to length of strs
  const l = strs.length,
    strl = strs[0].length;
  // set used to array of length l, fill with false
  const used = Array(l).fill(false);
  // set queue to empty array
  const queue = [];
  // set res to 0
  let res = 0,
    cur,
    diff;

  for (let i = 0; i < l; i++) {
    // if used[i] is false, increment res and push strs[i] into queue
    if (!used[i]) {
      res++;
      // set used[i] to true
      queue.push(strs[i]);
    }

    // WHILE queue is not empty
    while (queue.length > 0) {
      // pop from queue and set to cur
      cur = queue.pop();
      for (let j = 0; j < l; j++) {
        if (!used[j]) {
          // check cur and strl is similar or not
          // if diff > 2: they are not similar, otherwise: add strs[j] into queue
          diff = 0;
          for (let k = 0; k < strl; k++) {
            // IF cur[k] is not equal to strs[j][k] and increment diff > 2, break
            if (cur[k] !== strs[j][k] && ++diff > 2) break;
          }
          if (diff <= 2) {
            // set used[j] to true
            used[j] = true;
            // push strs[j] into queue
            queue.push(strs[j]);
          }
        }
      }
    }
  }
  return res;
};
```
