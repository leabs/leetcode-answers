---
layout: post
title: 997. Find the Town Judge
date: 2023-01-23 09:19 -0500
difficulty: easy
comments: true
---

In a town, there are `n` people labeled from `1` to `n`. There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

The town judge `trusts` nobody.

Everybody (except for the town judge) trusts the town judge.

There is exactly one person that satisfies properties **1** and **2**.

You are given an array `trust` where `trust[i] = [ai, bi]` representing that the person labeled `ai` trusts the person labeled `bi`.

Return the _label of the town judge if the town judge exists and can be identified, or return_ `-1` _otherwise_.

<pre><strong>Input:</strong> n = 2, trust = [[1,2]]
<strong>Output:</strong> 2
</pre>

```javascript
/**
 * @param {number} n
 * @param {number[][]} trust
 * @return {number}
 */
var findJudge = function (n, trust) {
  let arr = new Array(n).fill(0);
  let count = new Array(n).fill(0);
  for (let [x, y] of trust) {
    arr[x - 1] = 1;
    count[y - 1]++;
  }
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] == 0 && count[i] == n - 1) {
      return i + 1;
    }
  }
  return -1;
};
```
