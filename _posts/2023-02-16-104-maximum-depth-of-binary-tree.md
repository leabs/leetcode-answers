---
layout: post
title: 104. Maximum Depth of Binary Tree
date: 2023-02-16 08:49 -0500
difficulty: easy
comments: true
---

Given the `root` of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## Example

```javascript
Input: root = [3,9,20,null,null,15,7]
Output: 3
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
 * @return {number}
 */
var maxDepth = function (root) {
    //If the root is null, return 0
    if (root === null) return 0;
    //Return the maximum depth of the left and right subtrees plus 1
    return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};
```
