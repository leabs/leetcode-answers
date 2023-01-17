---
layout: post
title: "1061. Lexicographically Smallest Equivalent String"
date: 2023-01-14 07:35:33 -0500
comments: true
difficulty: medium
---

You are given two strings of the same length `s1` and `s2` and a string baseStr.

We say `s1[i]` and `s2[i]` are equivalent characters.

- For example, if `s1 = "abc"` and `s2 = "cde"`, then we have `'a' == 'c'`, `'b' == 'd'`, and `'c' == 'e'`.

Equivalent characters follow the usual rules of any equivalence relation:

- Reflexivity: `'a' == 'a'`.
- Symmetry: `'a' == 'b'` implies `'b' == 'a'`.
- Transitivity: `'a' == 'b'` and `'b' == 'c'` implies `'a' == 'c'`.

For example, given the equivalency information from `s1 = "abc"` and `s2 = "cde"`, `"acd"` and "aab" are equivalent strings of `baseStr = "eed"`, and `"aab"` is the lexicographically smallest equivalent string of `baseStr`.

Return the lexicographically smallest equivalent string of `baseStr` by using the equivalency information from `s1` and `s2`.

<pre><strong>Input:</strong> s1 = "parker", s2 = "morris", baseStr = "parser"
<strong>Output:</strong> "makkek"
<strong>Explanation:</strong> Based on the equivalency information in s1 and s2, we can group their characters as [m,p], [a,o], [k,r,s], [e,i].
The characters in each group are equivalent and sorted in lexicographical order.
So the answer is "makkek".
</pre>

```javascript
/**
 * @param {string} s1
 * @param {string} s2
 * @param {string} baseStr
 * @return {string}
 */
var smallestEquivalentString = function (s1, s2, baseStr) {
  //set new array for the 26 characters
  let arr = new Array(26);

  //fill the array with the characters
  for (let i = 0; i < arr.length; i++) {
    arr[i] = String.fromCharCode(i + 97);
  }
  //loop through the s1 and s2
  for (let i = 0; i < s1.length; i++) {
    let f = arr[s1[i].charCodeAt(0) - 97];
    let s = arr[s2[i].charCodeAt(0) - 97];
    if (f == s) continue;
    let replaceTo = "";
    let replaceFrom = "";
    //replace the smaller character with the bigger character
    if (f > s) {
      replaceTo = s;
      replaceFrom = f;
    }
    //replace the bigger character with the smaller character
    else {
      replaceTo = f;
      replaceFrom = s;
    }
    //loop through the array and replace the bigger character with the smaller character
    for (let i = 0; i < arr.length; i++) {
      if (arr[i] == replaceFrom) arr[i] = replaceTo;
    }
  }
  let res = "";
  //loop through the baseStr and replace the characters with the equivalent characters
  for (let i = 0; i < baseStr.length; i++) {
    res += arr[baseStr.charCodeAt(i) - 97];
  }
  return res;
};
```
