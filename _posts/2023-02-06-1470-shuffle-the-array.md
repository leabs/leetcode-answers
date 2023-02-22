---
layout: post
title: 1470. Shuffle the Array
date: 2023-02-06 10:18 -0500
difficulty: easy
comments: true
---
Given the array `nums` consisting of `2n` elements in the form `[x1,x2,...,xn,y1,y2,...,yn]`.

_Return the array in the form_ `[x1,y1,x2,y2,...,xn,yn]`.

## Example:
<pre><strong>Input:</strong> nums = [2,5,1,3,4,7], n = 3
<strong>Output:</strong> [2,3,5,4,1,7] 
<strong>Explanation:</strong> Since x<sub>1</sub>=2, x<sub>2</sub>=5, x<sub>3</sub>=1, y<sub>1</sub>=3, y<sub>2</sub>=4, y<sub>3</sub>=7 then the answer is [2,3,5,4,1,7].
</pre>

## Solution

```javascript
/**
 * @param {number[]} nums
 * @param {number} n
 * @return {number[]}
 */
var shuffle = function(nums, n) {
    //Combine the nums array with n in index order
    return nums.reduce((acc,curr,i) => {
        //Check if i is less than n
        if(i < n){
            //Push the current element and the element at n+i index
            acc.push(curr,nums[n+i]);
        }
        //Return the acc
        return acc;
    },[]);
};
```