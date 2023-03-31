---
layout: post
title: 1444. Number of Ways of Cutting a Pizza
date: 2023-03-31 08:37 -0400
difficulty: hard
comments: true
---

Given a rectangular pizza represented as a `rows x cols` matrix containing the following characters: `'A'` (an apple) and `'.'` (empty cell) and given the integer `k`. You have to cut the pizza into `k` pieces using `k-1` cuts.

For each cut you choose the direction: vertical or horizontal, then you choose a cut position at the cell boundary and cut the pizza into two pieces. If you cut the pizza vertically, give the left part of the pizza to a person. If you cut the pizza horizontally, give the upper part of the pizza to a person. Give the last piece of pizza to the last person.

_Return the number of ways of cutting the pizza such that each piece contains **at least** one apple_. Since the answer can be a huge number, return this modulo 10^9 + 7.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-31.png" alt="Example flow image" />

```javascript
Input: pizza = ["A..","AAA","..."], k = 3
Output: 3
Explanation: The figure above shows the three ways to cut the pizza. Note that pieces must contain at least one apple.
```

## Solution

Great solution found [here](https://leetcode.com/problems/number-of-ways-of-cutting-a-pizza/solutions/3360878/simple-javascript-solution/?orderBy=most_votes&languageTags=javascript).

```javascript
/**
 * @param {string[]} pizza
 * @param {number} k
 * @return {number}
 */
var ways = function (pizza, k) {
  //Create a 2D array to store the number of apples in each cell
  let m = pizza.length,
    n = pizza[0].length,
    mod = 10 ** 9 + 7;
  //Create a 2D array to store the number of apples in each cell
  let appleCount = Array(m + 1)
    .fill(0)
    .map(() => Array(n + 1).fill(0));
  //Create a 3D array to store the number of ways to cut the pizza
  let memo = Array(m)
    .fill(0)
    .map(() =>
      Array(n)
        .fill(0)
        .map(() => Array(k + 1).fill(-1))
    );
  for (let i = m - 1; i >= 0; i--) {
    for (let j = n - 1; j >= 0; j--) {
      //If the current cell is an apple, add 1 to the number of apples in the cell
      let curr = pizza[i][j] === "A" ? 1 : 0;
      //
      appleCount[i][j] =
        appleCount[i][j + 1] +
        appleCount[i + 1][j] -
        appleCount[i + 1][j + 1] +
        curr;
    }
  }
  return dp(0, 0, k);

  function dp(i, j, k) {
    //If there are no apples in the current cell, return 0
    if (k === 1) return appleCount[i][j] > 0 ? 1 : 0;
    if (appleCount[i][j] === 0) return 0;
    //If the number of ways to cut the pizza is already calculated, return the value
    if (memo[i][j][k] !== -1) return memo[i][j][k];

    let ans = 0;
    //Cut the pizza vertically
    for (let newRow = i; newRow < m - 1; newRow++) {
      //If the top piece has no apples, continue
      if (appleCount[newRow + 1][j] === appleCount[i][j]) continue;
      // top piece has no apples
      ans = (ans + dp(newRow + 1, j, k - 1)) % mod;
    }
    //Cut the pizza horizontally
    for (let newCol = j; newCol < n - 1; newCol++) {
      //If the left piece has no apples, continue
      if (appleCount[i][newCol + 1] === appleCount[i][j]) continue;
      // left piece has no apples
      ans = (ans + dp(i, newCol + 1, k - 1)) % mod;
    }
    return (memo[i][j][k] = ans);
  }
};
```
