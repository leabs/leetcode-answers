---
layout: post
title: 946. Validate Stack Sequences
date: 2023-04-13 08:43 -0400
difficulty: medium
comments: true
---

Given two integer arrays `pushed` and `popped` each with distinct values, return `true` if this could have been the result of a sequence of push and pop operations on an initially empty stack, or `false` otherwise.

## Example

```javascript
Input: pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
Output: true
Explanation: We might do the following sequence:
push(1), push(2), push(3), push(4),
pop() -> 4,
push(5),
pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

## Solution

```javascript
/**
 * @param {number[]} pushed
 * @param {number[]} popped
 * @return {boolean}
 */
var validateStackSequences = function (pushed, popped) {
  // If the lengths of the arrays are not equal, return false
  if (pushed.length !== popped.length) return false;
  let stack = [];
  let i = 0;
  for (let j = 0; j < pushed.length; j++) {
    // Push the pushed array to the stack
    stack.push(pushed[j]);
    while (stack.length && stack[stack.length - 1] === popped[i]) {
      stack.pop();
      i++;
    }
  }
  return stack.length === 0;
};
```
