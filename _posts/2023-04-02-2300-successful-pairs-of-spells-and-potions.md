---
layout: post
title: 2300. Successful Pairs of Spells and Potions
date: 2023-04-02 09:08 -0400
difficulty: medium
comments: true
---

You are given two positive integer arrays `spells` and `potions`, of length `n` and `m` respectively, where `spells[i]` represents the strength of the `ith` spell and `potions[j]` represents the strength of the `jth` potion.

You are also given an integer `success`. A spell and potion pair is considered successful if the product of their strengths is at least `success`.

Return an integer array `pairs` of length `n` where `pairs[i]` is the number of potions that will form a successful pair with the `ith` spell.

## Example

```javascript
Input: spells = [5,1,3], potions = [1,2,3,4,5], success = 7
Output: [4,0,3]
Explanation:
- 0th spell: 5 * [1,2,3,4,5] = [5,10,15,20,25]. 4 pairs are successful.
- 1st spell: 1 * [1,2,3,4,5] = [1,2,3,4,5]. 0 pairs are successful.
- 2nd spell: 3 * [1,2,3,4,5] = [3,6,9,12,15]. 3 pairs are successful.
Thus, [4,0,3] is returned.
```

## Solution

```javascript
/**
 * @param {number[]} spells
 * @param {number[]} potions
 * @param {number} success
 * @return {number[]}
 */
var successfulPairs = function (spells, potions, success) {
  //Return an integer array `pairs` of length `n` where `pairs[i]` is the number of potions that will form a successful pair with the `ith` spell.

  // Initialize an empty array
  let res = [];
  //Sort postions
  potions.sort((a, b) => a - b);
  //For spells.length
  for (let i = 0; i < spells.length; i++) {
    //Binary search
    let h = potions.length - 1,
      l = 0,
      mid;
    while (l <= h) {
      //Find the first potion that is greater than or equal to success
      mid = ~~(l + (h - l) / 2);
      //If the product is greater than or equal to success, then we can reduce the potion
      if (spells[i] * potions[mid] >= success) h = mid - 1;
      //Else we need to increase the potion
      else l = mid + 1;
    }
    //Store the result
    res[i] = potions.length - 1 - h;
  }
  //Return res
  return res;
};
```
