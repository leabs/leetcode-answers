---
layout: post
title: 101. Symmetric Tree
date: 2023-03-13 08:36 -0400
difficulty: easy
comments: true
---

Given the `root` of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

## Example

<img src="{{ site.baseurl }}/assets/images/mar-13.jpg" alt="Example tree image" />

```javascript
Input: root = [1, 2, 2, 3, 4, 4, 3];
Output: true;
```

## Solution

Great solution [here](https://leetcode.com/problems/symmetric-tree/solutions/2423766/easy-0-ms-100-fully-explained-java-c-python-js-python3/?orderBy=hot&languageTags=javascript) in multiple langauges.

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
var isSymmetric = function (root) {
  // Special case...
  if (!root) return true;
  // Return the function recursively...
  return isSame(root.left, root.right);
};
// A tree is called symmetric if the left subtree must be a mirror reflection of the right subtree...
var isSame = function (leftroot, rightroot) {
  // If both root nodes are null pointers, return true...
  // If exactly one of them is a null node, return false...
  // If root nodes haven't same value, return false...
  if (
    (!leftroot && rightroot) ||
    (leftroot && !rightroot) ||
    (leftroot && rightroot && leftroot.val !== rightroot.val)
  )
    return false;
  // Return true if the values of root nodes are same and left as well as right subtrees are symmetric...
  if (leftroot && rightroot)
    return (
      isSame(leftroot.left, rightroot.right) &&
      isSame(leftroot.right, rightroot.left)
    );
  return true;
};
```
