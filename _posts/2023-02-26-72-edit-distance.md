---
layout: post
title: 72. Edit Distance
date: 2023-02-26 08:00 -0500
difficulty: hard
comments: true
---

Given two strings `word1` and `word2`, return the minimum number of operations required to convert `word1` to `word2`.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

## Example

```javascript
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation:
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

Great solution found [here](https://leetcode.com/problems/edit-distance/solutions/428527/javascript-solution/?orderBy=hot&languageTags=javascript)

## Solution

```javascript
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function (word1, word2) {
  let dp = Array(word1.length + 1)
    //Fill the array with null
    .fill(null)
    //Map over the array and fill it with an array of word2.length + 1
    .map(() => Array(word2.length + 1).fill(0));

  for (let i = 0; i < dp.length; i++) {
    //Fill the first row with the index
    dp[i][0] = i;
  }

  for (let i = 0; i < dp[0].length; i++) {
    //Fill the first column with the index
    dp[0][i] = i;
  }
  //Recursive formula
  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      //If the characters are the same, then we don't need to do anything
      dp[i][j] = Math.min(
        dp[i - 1][j] + 1, // left
        dp[i][j - 1] + 1, // right
        dp[i - 1][j - 1] + (word1[i - 1] != word2[j - 1] ? 1 : 0) // diagonal
      );
    }
  }
  //Return the last element in the array
  return dp[dp.length - 1][dp[0].length - 1];
};
```
