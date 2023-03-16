---
layout: post
title: 106. Construct Binary Tree from Inorder and Postorder Traversal
date: 2023-03-16 12:19 -0400
difficulty: medium
comments: true
---

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return the binary tree.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-16.jpg" alt="Example tree image" />

```javascript
Input: (inorder = [9, 3, 15, 20, 7]), (postorder = [9, 15, 7, 20, 3]);
Output: [3, 9, 20, null, null, 15, 7];
```

# Solution

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
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function (inorder, postorder) {
  //if there are no more nodes, return null
  if (!inorder.length) return null;
  //the last node in postorder is the root
  let root = new TreeNode(postorder.pop());
  //find the index of the root in inorder
  let rootIdx = inorder.indexOf(root.val);
  //build the right and left subtrees
  root.right = buildTree(inorder.slice(rootIdx + 1), postorder);
  //the left subtree is the remaining nodes in inorder
  root.left = buildTree(inorder.slice(0, rootIdx), postorder);
  return root;
};
```
