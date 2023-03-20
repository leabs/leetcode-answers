---
layout: post
title: 605. Can Place Flowers
date: 2023-03-20 07:52 -0400
difficulty: easy
comments: true
---

You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in **adjacent** plots.

Given an integer array `flowerbed` containing `0`'s and `1`'s, where `0` means empty and `1` means not empty, and an integer `n`, return if `n` new flowers can be planted in the `flowerbed` without violating the no-adjacent-flowers rule.

## Example

```javascript
Input: (flowerbed = [1, 0, 0, 0, 1]), (n = 1);
Output: true;
```

## Solution

```javascript
/**
 * @param {number[]} flowerbed
 * @param {number} n
 * @return {boolean}
 */
var canPlaceFlowers = function (flowerbed, n) {
  // Loop through flowerbeds and check if there is a 0 and the previous and next are not 1
  for (let i = 0; i < flowerbed.length && n !== 0; i++) {
    if (
      // Check if the current flowerbed is 0 and the previous and next are not 1
      flowerbed[i] === 0 &&
      // Check if the previous flowerbed is not 1
      flowerbed[i - 1] !== 1 &&
      // Check if the next flowerbed is not 1
      flowerbed[i + 1] !== 1
    ) {
      n--;
      i++;
    }
  }
  return n === 0;
};
```
