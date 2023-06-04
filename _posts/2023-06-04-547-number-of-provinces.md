---
layout: post
title: 547. Number of Provinces
date: 2023-06-04 08:57 -0400
difficulty: medium
comments: true
---

There are `n` cities. Some of them are connected, while some are not. If city a is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A province is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the ith city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return the total number of **provinces**.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-4.jpg" alt="example image" width="300"/>

```javascript
Input: isConnected = [
  [1, 1, 0],
  [1, 1, 0],
  [0, 0, 1],
];
Output: 2;
```

## Solution

```javascript
/**
 * @param {number[][]} isConnected
 * @return {number}
 */
var findCircleNum = function (isConnected) {};
```
