---
layout: post
title: 1046. Last Stone Weight
date: 2023-04-24 08:44 -0400
difficulty: easy
comments: true
---

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones and smash them together**. Suppose the heaviest two stones have weights x and y with x <= y. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one stone** left.

Return _the weight of the last remaining stone_. If there are no stones left, return `0`.

## Example

```javascript
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation:
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of the last stone.
```

## Solution

Great recursive solution found [here](https://leetcode.com/problems/last-stone-weight/solutions/1470255/simple-javascript-soluton-recursion/?languageTags=javascript).

```javascript
/**
 * @param {number[]} stones
 * @return {number}
 */
var lastStoneWeight = function (stones) {
  //If there is only one stone left, return it
  if (stones.length < 2) return stones;
  //Sort the stones in ascending order
  stones.sort((a, b) => a - b);
  //Get the difference between the two heaviest stones
  let a = stones.pop();
  let b = stones.pop();
  //Push the difference back into the array
  stones.push(Math.abs(a - b));
  //Recursively call the function until there is only one stone left
  return lastStoneWeight(stones);
};
```
