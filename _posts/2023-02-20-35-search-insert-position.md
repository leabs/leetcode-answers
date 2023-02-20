---
layout: post
title: 35. Search Insert Position
date: 2023-02-20 09:36 -0500
difficulty: easy
comments: true
---

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

## Example

```javascript
Input: (nums = [1, 3, 5, 6]), (target = 5);
Output: 2;
```

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    //Detirmine if the target is in the array.
    let targetIndex = nums.indexOf(target);
    //If the target is in the array, return the index.
    if(targetIndex != -1){
        return targetIndex;
    }
    //If the target is not in the array, find the index where it would be inserted.
    for(let i = 0; i < nums.length; i++){
        if(target < nums[i]){
            return i;
        }
    }
    //If the target is greater than all the elements in the array, return the length of the array.
    return nums.length;
};
```
