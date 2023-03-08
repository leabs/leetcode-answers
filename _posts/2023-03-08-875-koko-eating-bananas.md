---
layout: post
title: 875. Koko Eating Bananas
date: 2023-03-08 08:05 -0500
difficulty: medium
comments: true
---

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer `k` such that she can eat all the bananas within `h` hours.

## Example

```javascript
Input: (piles = [3, 6, 7, 11]), (h = 8);
Output: 4;
```

## Solution

Helpful solution found [here](https://leetcode.com/problems/koko-eating-bananas/solutions/1703427/javascript-binary-search-explained/?orderBy=hot&languageTags=javascript).

```javascript
/**
 * @param {number[]} piles
 * @param {number} h
 * @return {number}
 */
const minEatingSpeed = (piles, h) => {
  //Set min and max speed
  let min = 1,
    max = Math.max(...piles),
    best = max;

  // Set time to eat all bananas at speed
  const time = (speed) =>
    piles.reduce((sum, pile) => sum + Math.ceil(pile / speed), 0);

  while (min <= max) {
    // Find the middle speed to prevent overflow
    const mid = Math.floor((min + max) / 2);

    // If we can eat all bananas in h hours, try to eat faster
    if (time(mid) <= h) {
      best = mid;
      max = mid - 1;
    } else min = mid + 1;
  }
  return best;
};
```
