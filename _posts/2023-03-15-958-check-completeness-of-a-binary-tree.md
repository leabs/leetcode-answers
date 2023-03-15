---
layout: post
title: 958. Check Completeness of a Binary Tree
date: 2023-03-15 14:02 -0400
difficulty: medium
comments: true
---

Given the `root` of a binary tree, determine if it is a complete binary tree.

In a complete binary tree, every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-15.png" alt="Example tree image" />

```javascript
Input: root = [1,2,3,4,5,6]
Output: true
Explanation: Every level before the last is full (ie. levels with node-values {1} and {2, 3}), and all nodes in the last level ({4, 5, 6}) are as far left as possible.
```

## Solution

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isCompleteTree = function (root) {
  //if any levels are empty, return false
  if (!root) return true;
  let queue = [root];
  let empty = false;
  while (queue.length) {
    let node = queue.shift();
    if (!node) empty = true;
    else {
      if (empty) return false;
      queue.push(node.left);
      queue.push(node.right);
    }
  }
  return true;
};
```
