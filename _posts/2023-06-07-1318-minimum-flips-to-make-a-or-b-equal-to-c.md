---
layout: post
title: 1318. Minimum Flips to Make a OR b Equal to c
date: 2023-06-07 07:58 -0400
difficulty: medium
comments: true
---

Given 3 positives numbers `a`, `b` and `c`. Return the minimum flips required in some bits of `a` and `b` to make ( `a` OR `b` == `c` ). (bitwise OR operation).

Flip operation consists of change any single bit 1 to 0 or change the bit 0 to 1 in their binary representation.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-7.png" alt="example chart image" width="300"/>

```javascript
Input: a = 2, b = 6, c = 5
Output: 3
Explanation: After flips a = 1 , b = 4 , c = 5 such that (a OR b == c)
```

## Solution

```javascript
var minFlips = function (a, b, c) {
  let flips = 0;
  while (a > 0 || b > 0 || c > 0) {
    let aBit = a & 1;
    let bBit = b & 1;
    let cBit = c & 1;
    if ((aBit | bBit) !== cBit) {
      if (cBit === 0) {
        flips += aBit + bBit;
      } else {
        flips += 1;
      }
    }
    a >>= 1;
    b >>= 1;
    c >>= 1;
  }
  return flips;
};
```
