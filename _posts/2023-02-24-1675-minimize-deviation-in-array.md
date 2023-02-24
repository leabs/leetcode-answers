---
layout: post
title: 1675. Minimize Deviation in Array
date: 2023-02-24 08:00 -0500
difficulty: hard
comments: true
---

You are given an array `nums` of `n` positive integers.

You can perform two types of operations on any element of the array any number of times:

- If the element is even, divide it by `2`.
  - For example, if the array is `[1,2,3,4]`, then you can do this operation on the last element, and the array will be `[1,2,3,2]`.
- If the element is odd, multiply it by `2`.
  - For example, if the array is `[1,2,3,4]`, then you can do this operation on the first element, and the array will be `[2,2,3,4]`.

The **deviation** of the array is the **maximum difference** between any two elements in the array.

Return the minimum deviation the array can have after performing some number of operations.

## Example

```javascript
Input: nums = [1,2,3,4]
Output: 1
Explanation: You can transform the array to [1,2,3,2], then to [2,2,3,2], then the deviation will be 3 - 2 = 1.
```

## Solution

Great solution [here](h<https://leetcode.com/problems/minimize-deviation-in-array/solutions/1042804/javascript-using-max-priority-queue-with-comments/?orderBy=hot&languageTags=javascript)>

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var minimumDeviation = function (nums) {
  // https://github.com/datastructures-js/priority-queue
  const mpq = new MaxPriorityQueue();

  // Convert all the numbers to even and enqueue them
  nums.forEach((num) => {
    if (num % 2 !== 0) {
      const value = num * 2;

      mpq.enqueue(value, value);
    } else {
      mpq.enqueue(num, num);
    }
  });

  // Get difference between max and min values
  let deviation = mpq.front().element - mpq.back().element;

  // Loop until we have any max even number left in the queue
  while (mpq.front().element % 2 === 0) {
    // Get max even value
    const { element } = mpq.dequeue();

    // Convert it to odd number and enqueue again
    mpq.enqueue(element / 2, element / 2);

    // Get minimum between previous deviation and after above conversion
    deviation = Math.min(deviation, mpq.front().element - mpq.back().element);
  }

  return deviation;
};
```
