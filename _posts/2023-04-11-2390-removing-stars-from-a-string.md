---
layout: post
title: 2390. Removing Stars From a String
date: 2023-04-11 08:14 -0400
difficulty: medium
comments: true
---

You are given a string `s`, which contains stars `*`.

In one operation, you can:

- Choose a star in `s`.
- Remove the closest **non-star** character to its left, as well as remove the star itself.
- Return the string after all stars have been removed.

Note:

- The input will be generated such that the operation is always possible.
- It can be shown that the resulting string will always be unique.

## Example

```javascript
Input: s = "leet**cod*e"
Output: "lecoe"
Explanation: Performing the removals from left to right:
- The closest character to the 1st star is 't' in "leet**cod*e". s becomes "lee*cod*e".
- The closest character to the 2nd star is 'e' in "lee*cod*e". s becomes "lecod*e".
- The closest character to the 3rd star is 'd' in "lecod*e". s becomes "lecoe".
There are no more stars, so we return "lecoe".
```

## Solution

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var removeStars = function (s) {
  //FOR the lenght of the string
  for (let i = 0; i < s.length; i++) {
    //IF the character is a star
    if (s[i] === "*") {
      //Remove the closest non-star character to its left and the star itself
      s = s.slice(0, i - 1) + s.slice(i + 1);
      //Decrement i by 2 to account for the removed characters
      i -= 2;
    }
  }
  return s;
};
```
