---
layout: post
title: 989. Add to Array-Form of Integer
date: 2023-02-15 08:47 -0500
difficulty: easy
comments: true
---

The array-form of an integer `num` is an array representing its digits in left to right order.

For example, for `num = 1321`, the array form is `[1,3,2,1]`.

Given `num`, the **array-form** of an integer, and an integer `k`, return the _array-form_ of the integer `num + k`.

## Example

```javascript
Input: num = [1,2,0,0], k = 34
Output: [1,2,3,4]
Explanation: 1200 + 34 = 1234
```


```javascript
/**
 * @param {number[]} num
 * @param {number} k
 * @return {number[]}
 */
var addToArrayForm = function (num, k) {
    //Add num and k as arrays
    let carry = 0;
    //Start from the end of the array
    let i = num.length - 1;
    while (k > 0 || carry > 0) {
        //Add the last digit of k to the last digit of num
        let sum = k % 10 + carry;
        //If there are still digits in num, add them to sum
        if (i >= 0) {
            //Add the last digit of num to sum
            sum += num[i];
            //Replace the last digit of num with the sum
            num[i] = sum % 10;
            i--;
        } else {
            //If there are no more digits in num, add the sum to the beginning of num
            num.unshift(sum % 10);
        }
        //Update carry
        carry = Math.floor(sum / 10);
        //Update k
        k = Math.floor(k / 10);
    }
    //Return num
    return num;

};
```
