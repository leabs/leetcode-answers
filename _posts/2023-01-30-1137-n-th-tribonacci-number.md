---
layout: post
title: 1137. N-th Tribonacci Number
date: 2023-01-30 09:16 -0500
difficulty: easy
comments: true
---

The Tribonacci sequence Tn is defined as follows:

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given `n`, return the value of Tn.

## Example

<pre><strong>Input:</strong> n = 4
<strong>Output:</strong> 4
<strong>Explanation:</strong>
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
</pre>

## Solution

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var tribonacci = function(n) {
    //Declare an array of size n+1 and fill it with 0
    let dp = new Array(n+1).fill(0);
    dp[1] = 1
    dp[2] = 1;
    for(let i =3; i<=n; i++){
        //The tribonacci number at index i is the sum of the previous 3 tribonacci numbers
        dp[i] = dp[i-1] + dp[i-2] +dp[i-3]
    }
    //Return the tribonacci number at index n
    return dp[n]
};
```
