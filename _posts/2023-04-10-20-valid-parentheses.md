---
layout: post
title: 20. Valid Parentheses
date: 2023-04-10 08:55 -0400
difficulty: easy
comments: true
---

Given a string s containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.
- Every close bracket has a corresponding open bracket of the same type.

## Example

```javascript
Input: s = "()";
Output: true;
```

## Solution

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  //Return false if string is odd
  if (s.length % 2 !== 0) return false;
  //Return false if the first character is a closing bracket
  if (s[0] === ")" || s[0] === "}" || s[0] === "]") return false;
  //Create a stack
  let stack = [];
  //Loop through string
  for (let i = 0; i < s.length; i++) {
    //If the character is an opening bracket, push it to the stack
    if (s[i] === "(" || s[i] === "{" || s[i] === "[") {
      stack.push(s[i]);
    }
    //If the character is a closing bracket, check if it matches the last opening bracket in the stack
    if (s[i] === ")") {
      if (stack[stack.length - 1] === "(") {
        stack.pop();
      } else {
        return false;
      }
    }
    if (s[i] === "}") {
      if (stack[stack.length - 1] === "{") {
        stack.pop();
      } else {
        return false;
      }
    }
    if (s[i] === "]") {
      if (stack[stack.length - 1] === "[") {
        stack.pop();
      } else {
        return false;
      }
    }
  }
  //If the stack is empty, return true
  if (stack.length === 0) {
    return true;
  }
  //Otherwise, return false
  return false;
};
```
