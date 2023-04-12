---
layout: post
title: 71. Simplify Path
date: 2023-04-12 08:42 -0400
difficulty: medium
comments: true
---

Given a string `path`, which is an absolute path (starting with a slash `'/'`) to a file or directory in a Unix-style file system, convert it to the simplified canonical path.

In a Unix-style file system, a period `'.'` refers to the current directory, a double period `'..'` refers to the directory up a level, and any multiple consecutive slashes (i.e. `'//'`) are treated as a single slash '/'. For this problem, any other format of periods such as `'...'` are treated as file/directory names.

The **canonical path** should have the following format:

- The path starts with a single slash `'/'`.
- Any two directories are separated by a single slash `'/'`.
- The path does not end with a trailing `'/'`.
- The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period `'.'` or double period `'..'`)

_Return the simplified **canonical path**_.

## Example

```javascript
Input: path = "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
```

## Solution

```javascript
/**
 * @param {string} path
 * @return {string}
 */
var simplifyPath = function (path) {
  // Declare a stack to hold the path
  let stack = [];
  // Split the path into an array
  let pathArr = path.split("/");
  for (let i = 0; i < pathArr.length; i++) {
    // If the path is a double period, pop the stack
    if (pathArr[i] === "..") {
      // If the stack is empty, do nothing
      stack.pop();
      // If the path is a single period or empty, do nothing
    } else if (pathArr[i] !== "." && pathArr[i] !== "") {
      // Otherwise push the path to the stack
      stack.push(pathArr[i]);
    }
  }
  // Return the stack joined with a slash
  return "/" + stack.join("/");
};
```
