---
layout: post
title: 1822. Sign of the Product of an Array
date: 2023-05-02 09:01 -0400
difficulty: easy
comments: true
---

There is a function `signFunc(x)` that returns:

- `1` if `x` is positive.
- `-1` if `x` is negative.
- `0` if `x` is equal to `0`.

You are given an integer array `nums`. Let `product` be the product of all values in the array `nums`.

Return `signFunc(product)`.

## Example

```javascript
Input: nums = [-1,-2,-3,-4,3,2,1]
Output: 1
Explanation: The product of all values in the array is 144, and signFunc(144) = 1
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var arraySign = function (nums) {
  //Set product to 1
  let product = 1;
  //FOR loop to iterate through nums array
  for (let i = 0; i < nums.length; i++) {
    //Set product to product * nums[i]
    product = product * nums[i];
  }
  //IF product is greater than 0
  if (product > 0) {
    //Return 1
    return 1;
    //ELSE IF product is less than 0
  } else if (product < 0) {
    //Return -1
    return -1;
    //ELSE
  } else {
    //Return 0
    return 0;
  }
};
```
