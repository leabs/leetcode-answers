---
layout: post
title: 2348. Number of Zero-Filled Subarrays
date: 2023-03-21 08:47 -0400
difficulty: medium
comments: true
---

Given an integer array `nums`, return the number of **subarrays** filled with `0`.

A **subarray** is a contiguous non-empty sequence of elements within an array.

## Example

```javascript
Input: nums = [1,3,0,0,2,0,0,4]
Output: 6
Explanation: 
There are 4 occurrences of [0] as a subarray.
There are 2 occurrences of [0,0] as a subarray.
There is no occurrence of a subarray with a size more than 2 filled with 0. Therefore, we return 6.
```

## Example 2

```javascript
Input: nums = [0,0,0,2,0,0]
Output: 9
Explanation:
There are 5 occurrences of [0] as a subarray.
There are 3 occurrences of [0,0] as a subarray.
There is 1 occurrence of [0,0,0] as a subarray.
There is no occurrence of a subarray with a size more than 3 filled with 0. Therefore, we return 9.
```

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var zeroFilledSubarray = function(nums) {
    //Declare Counter and static 0 counter
    let count = 0;
    let zeroCount = 0;
    //Loop through nums
    for (let i = 0; i < nums.length; i++) {
        //If the current number is 0, increment the zero counter
        if (nums[i] === 0) {
        zeroCount++;
        } else {
            //If the current number is not 0, add the number of subarrays to the counter
        count += (zeroCount * (zeroCount + 1)) / 2;
        zeroCount = 0;
        }
    }
    //Add the number of subarrays to the counter
    count += (zeroCount * (zeroCount + 1)) / 2;
    return count;  
};
```
