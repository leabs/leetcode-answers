---
layout: post
title: 1372. Longest ZigZag Path in a Binary Tree
date: 2023-04-19 09:27 -0400
difficulty: medium
comments: true
---

You are given the `root` of a binary tree.

A ZigZag path for a binary tree is defined as follow:

- Choose **any** node in the binary tree and a direction (right or left).
- If the current direction is right, move to the right child of the current node; otherwise, move to the left child.
- Change the direction from right to left or from left to right.
- Repeat the second and third steps until you can't move in the tree.

Zigzag length is defined as the number of nodes visited - 1. (A single node has a length of 0).

Return the longest **ZigZag** path contained in that tree.

## Example

<img src="{{ site.baseurl }}/assets/images/apr-19.png" alt="Example tree image" />

```javascript
Input: root = [1,null,1,1,1,null,null,1,1,null,1,null,null,null,1,null,1]
Output: 3
Explanation: Longest ZigZag path in blue nodes (right -> left -> right).
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
let ans = 0;

//dfs to find the longest zigzag path
var dfs = (root, left, steps) => {
  if (root == undefined) {
    return;
  }
  //update the longest zigzag path
  ans = Math.max(ans, steps);

  //if left is true, we are going left to right
  if (left) {
    dfs(root.left, !left, steps + 1);
    dfs(root.right, left, 1);
  }
  //if left is false, we are going right to left
  else {
    dfs(root.left, left, 1);
    dfs(root.right, !left, steps + 1);
  }
};

var longestZigZag = function (root) {
  ans = 0;
  //start from left and right
  dfs(root, true, 0);
  //start from right and left
  dfs(root, false, 0);

  return ans;
};
```
