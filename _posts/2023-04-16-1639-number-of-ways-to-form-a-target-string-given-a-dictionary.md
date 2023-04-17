---
layout: post
title: 1639. Number of Ways to Form a Target String Given a Dictionary
date: 2023-04-16 09:21 -0400
difficulty: hard
comments: true
---

You are given a list of strings of the **same length** `words` and a string `target`.

Your task is to form `target` using the given `words` under the following rules:

- `target` should be formed from left to right.
- To form the `ith` character **(0-indexed)** of `target`, you can choose the `kth` character of the `jth` string in `words` if `target[i] = words[j][k]`.
- Once you use the `kth` character of the `jth` string of `words`, you **can no longer** use the xth character of any string in words where x <= k. In other words, all characters to the left of or at index `k` become unusuable for every string.
- Repeat the process until you form the string `target`.

**Notice** that you can use **multiple characters** from the **same string** in `words` provided the conditions above are met.

Return the number of ways to form `target` from `words`. Since the answer may be too large, return it modulo `109 + 7`.

## Example

```javascript
Input: words = ["acca","bbbb","caca"], target = "aba"
Output: 6
Explanation: There are 6 ways to form target.
"aba" -> index 0 ("acca"), index 1 ("bbbb"), index 3 ("caca")
"aba" -> index 0 ("acca"), index 2 ("bbbb"), index 3 ("caca")
"aba" -> index 0 ("acca"), index 1 ("bbbb"), index 3 ("acca")
"aba" -> index 0 ("acca"), index 2 ("bbbb"), index 3 ("acca")
"aba" -> index 1 ("caca"), index 2 ("bbbb"), index 3 ("acca")
"aba" -> index 1 ("caca"), index 2 ("bbbb"), index 3 ("caca")
```

## Solution

Great solution found [here](https://leetcode.com/problems/number-of-ways-to-form-a-target-string-given-a-dictionary/solutions/3423644/javascript-solution-with-memoization/?languageTags=javascript).

```javascript
function solve(i, j, freq, target, t) {
  //Define mod, m, k
  const MOD = 1000000007;
  const m = target.length;
  const k = freq[0].length;

  if (i == m) return 1;

  if (j == k) return 0;

  if (t[i][j] != -1) return t[i][j];

  // Define not_taken as the number of ways to form target[i] using words[j] and the characters to the left of words[j]
  const not_taken = solve(i, j + 1, freq, target, t) % MOD;

  //Define taken as the number of ways to form target[i] using words[j] and the characters to the right of words[j]
  const taken =
    (freq[target[i].charCodeAt() - 97][j] *
      solve(i + 1, j + 1, freq, target, t)) %
    MOD;
  //Return the sum of not_taken and taken
  return (t[i][j] = (not_taken + taken) % MOD);
}

//Function that returns the number of ways to form target from words
function numWays(words, target) {
  const k = words[0].length;
  const m = target.length;

  const freq = Array.from(new Array(26), () => Array(k).fill(0));

  for (let col = 0; col < k; col++) {
    for (let word of words) {
      //Increment the frequency of the character at index col in word by 1
      freq[word.charCodeAt(col) - 97][col]++;
    }
  }

  const t = Array(m)
    .fill(-1)
    .map(() => Array(k).fill(-1));

  return solve(0, 0, freq, target, t);
}
```
