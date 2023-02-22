---
layout: post
title: 226. Invert Binary Tree
date: 2023-02-18 09:09 -0500
difficulty: easy
comments: true
---

Given the `root` of a binary tree, invert the tree, and return its root.

## Example

```javascript
Input: root = [4, 2, 7, 1, 3, 6, 9];
Output: [4, 7, 2, 9, 6, 3, 1];
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
 * @return {TreeNode}
 */
var invertTree = function (root) {
  //If root is null, return null.
    if (root == null) return null;
    //Swap the left and right nodes.
    let temp = root.left;
    root.left = root.right;
    root.right = temp;
    //Recursively invert the left and right subtrees.
    invertTree(root.left);
    invertTree(root.right);
    //Return the root.
    return root;
};
```
