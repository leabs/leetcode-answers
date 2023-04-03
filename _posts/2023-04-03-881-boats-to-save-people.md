---
layout: post
title: 881. Boats to Save People
date: 2023-04-03 09:16 -0400
difficulty: medium
comments: true
---

You are given an array `people` where `people[i]` is the weight of the `ith` person, and an infinite number of boats where each boat can carry a maximum weight of `limit`. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most `limit`.

Return the minimum number of boats to carry every given person.

## Example

```javascript
Input: people = [1,2], limit = 3
Output: 1
Explanation: 1 boat (1, 2)
```

## Solution

```javascript
/**
 * @param {number[]} people
 * @param {number} limit
 * @return {number}
 */
var numRescueBoats = function (people, limit) {
  //Sort people
  people.sort((a, b) => a - b);
  //Initialize res
  let res = 0;
  //For people.length check if the sum of the first and last person is greater than limit
  for (let i = 0, j = people.length - 1; i <= j; j--) {
    //If the sum is greater than limit, then we need to increase the boat
    if (people[i] + people[j] > limit) res++;
    //Else we can reduce the boat
    else {
      res++;
      i++;
    }
  }
  //Return res
  return res;
};
```
