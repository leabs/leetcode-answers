---
layout: post
title: 2336. Smallest Number in Infinite Set
date: 2023-04-25 08:55 -0400
difficulty: medium
comments: true
---

You have a set which contains all positive integers `[1, 2, 3, 4, 5, ...]`.

Implement the `SmallestInfiniteSet` class:

- `SmallestInfiniteSet()` Initializes the **SmallestInfiniteSet** object to contain **all** positive integers.
- `int popSmallest()` **Removes** and returns the smallest integer contained in the infinite set.
- `void addBack(int num)` **Adds** a positive integer `num` back into the infinite set, if it is not already in the infinite set.

## Example

```javascript
Input
["SmallestInfiniteSet", "addBack", "popSmallest", "popSmallest", "popSmallest", "addBack", "popSmallest", "popSmallest", "popSmallest"]
[[], [2], [], [], [], [1], [], [], []]
Output
[null, null, 1, 2, 3, null, 1, 4, 5]

Explanation
SmallestInfiniteSet smallestInfiniteSet = new SmallestInfiniteSet();
smallestInfiniteSet.addBack(2);    // 2 is already in the set, so no change is made.
smallestInfiniteSet.popSmallest(); // return 1, since 1 is the smallest number, and remove it from the set.
smallestInfiniteSet.popSmallest(); // return 2, and remove it from the set.
smallestInfiniteSet.popSmallest(); // return 3, and remove it from the set.
smallestInfiniteSet.addBack(1);    // 1 is added back to the set.
smallestInfiniteSet.popSmallest(); // return 1, since 1 was added back to the set and
                                   // is the smallest number, and remove it from the set.
smallestInfiniteSet.popSmallest(); // return 4, and remove it from the set.
smallestInfiniteSet.popSmallest(); // return 5, and remove it from the set.
```

## Solution

```javascript
var SmallestInfiniteSet = function () {
  //Initializes the SmallestInfiniteSet object to contain all positive integers.
  this.arr = new Array(1001).fill(true);
};

/**
 * @return {number}
 */
SmallestInfiniteSet.prototype.popSmallest = function () {
  //Removes and returns the smallest integer contained in the infinite set.
  for (let i = 1; i < this.arr.length; i++) {
    if (this.arr[i]) {
      this.arr[i] = false;
      return i;
    }
  }
  return null;
};

/**
 * @param {number} num
 * @return {void}
 */
SmallestInfiniteSet.prototype.addBack = function (num) {
  //Adds a positive integer num back into the infinite set, if it is not already in the infinite set.
  this.arr[num] = true;
};

/**
 * Your SmallestInfiniteSet object will be instantiated and called as such:
 * var obj = new SmallestInfiniteSet()
 * var param_1 = obj.popSmallest()
 * obj.addBack(num)
 */
```
