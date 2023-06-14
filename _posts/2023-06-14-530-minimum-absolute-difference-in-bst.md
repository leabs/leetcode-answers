---
layout: post
title: 530. Minimum Absolute Difference in BST
date: 2023-06-14 07:50 -0400
difficulty: easy
comments: true
---

Given the `root` of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-14.jpg" alt="example tree image" width="300"/>

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
var getMinimumDifference = function (root) {
  //convert root to sorted array
  const arr = [];
  const traverse = (node) => {
    if (node.left) traverse(node.left);
    arr.push(node.val);
    if (node.right) traverse(node.right);
  };
  traverse(root);
  //set min to Infinity
  let min = Infinity;
  //loop through array
  for (let i = 0; i < arr.length - 1; i++) {
    //set diff to difference between current and next element
    const diff = arr[i + 1] - arr[i];
    //if diff is less than min, set min to diff
    if (diff < min) min = diff;
  }
  return min;
};
```
