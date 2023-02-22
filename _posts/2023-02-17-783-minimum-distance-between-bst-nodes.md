---
layout: post
title: 783. Minimum Distance Between BST Nodes
date: 2023-02-17 08:37 -0500
difficulty: easy
comments: true
---

Given the `root` of a Binary Search Tree (BST), return the _minimum difference between the values of any two different nodes in the tree._

## Example

```javascript
Input: root = [4, 2, 6, 1, 3];
Output: 1;
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
var minDiffInBST = function (root) {
  //If root is null, return.
  if (root == null) return;

  //Declare variables for the current node, the previous node, and the minimum difference.
  let s = [];
  let curr = root;
  let prev = null;
  let min = Infinity;
  //Iterate through the tree using an in-order traversal.
  while (curr !== null || s.length > 0) {
    //Push all left nodes to the stack.
    while (curr !== null) {
      s.push(curr);
      //Move to the left node.
      curr = curr.left;
    }
    //Pop the last node from the stack.
    curr = s.pop();

    //If the previous node is not null, compare the difference between the current node and the previous node with the minimum difference.
    if (prev) {
      //If the difference is less than the minimum difference, update the minimum difference.
      min = Math.min(curr.val - prev.val, min);
    }
    //Update the previous node.
    prev = curr;

    //Move to the right node.
    curr = curr.right;
  }
  //Return the minimum difference.
  return min;
};
```
