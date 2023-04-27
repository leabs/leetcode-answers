---
layout: post
title: 319. Bulb Switcher
date: 2023-04-27 08:40 -0400
difficulty: medium
comments: true
---

There are `n` bulbs that are initially off. You first turn on all the bulbs, then you turn off every second bulb.

On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the `ith` round, you toggle every `i` bulb. For the `nth` round, you only toggle the last bulb.

Return the number of bulbs that are on after `n` rounds.

## Example

<img src="{{ site.baseurl }}/assets/images/apr-27.jpg" alt="Bulb image" />

```javascript
Input: n = 3
Output: 1
Explanation: At first, the three bulbs are [off, off, off].
After the first round, the three bulbs are [on, on, on].
After the second round, the three bulbs are [on, off, on].
After the third round, the three bulbs are [on, off, off].
So you should return 1 because there is only one bulb is on.
```

## Solution

Brilliant one line solution [here](https://leetcode.com/problems/bulb-switcher/solutions/376978/javascript-one-line-solution/?orderBy=most_votes&languageTags=javascript).

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var bulbSwitch = function (n) {
  // Return the square root of n to get the number of bulbs that are on
  return parseInt(Math.sqrt(n));
};
```
