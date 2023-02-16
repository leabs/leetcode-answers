---
layout: post
title: 1071. Greatest Common Divisor of Strings
date: 2023-02-01 09:09 -0500
difficulty: easy
comments: true
---
For two strings `s` and `t`, we say "`t` divides `s`" if and only if `s = t + ... + t` (i.e., `t` is concatenated with itself one or more times).

Given two strings `str1` and `str2`, return the largest string `x` such that `x` divides both `str1` and `str2`.

## Example
<pre><strong>Input:</strong> str1 = "ABCABC", str2 = "ABC"
<strong>Output:</strong> "ABC"
</pre>

Great solution [here.](https://leetcode.com/problems/greatest-common-divisor-of-strings/solutions/2641769/js-very-easy-solution-faster-than-99/?orderBy=hot&languageTags=javascript)

```javascript
// Set up a function that checks if a string is divisible by another string
const isDivides = (long, short) => {
    const current = short;
    for (let i = 1; i < long.length/current.length; i++) {
        short+=current;
    }
    return short === long;
};

// Set up a function that returns the greatest common divisor of two strings
var gcdOfStrings = function(str1, str2) {
    // Set up a variable for the longer string and a variable for the shorter string
    const long = str1.length >= str2.length ? str1 : str2;
    // Set up a variable for the shorter string and a variable for the longer string
    const short = str1.length >= str2.length ? str2 : str1;

    // If the shorter string is divisible by the longer string, return the shorter string
    if (isDivides(long,short)) return short;

    // Set up a variable for the current string
    let currentStr = '';
    // Loop through the shorter string
    for (let i = Math.floor(short.length/2); i > 0; i--) {
        // Set the current string to the substring of the shorter string from 0 to i
        currentStr = short.substring(0, i);
        // If the current string is divisible by the shorter string and the longer string, return the current string
        if (isDivides(short, currentStr) && isDivides(long, currentStr)) return currentStr;
    }
    //return an empty string if no common divisor is found
    return '';
};

```