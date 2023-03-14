---
layout: post
title: 129. Sum Root to Leaf Numbers
date: 2023-03-14 08:49 -0400
difficulty: medium
comments: true
---

You are given the `root` of a binary tree containing digits from `0` to `9` only.

Each root-to-leaf path in the tree represents a number.

For example, the root-to-leaf path `1 -> 2 -> 3` represents the number `123`.
Return the total sum of all root-to-leaf numbers. Test cases are generated so that the answer will fit in a **32-bit** integer.

A **leaf** node is a node with no children.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-14.jpg" alt="Example tree image" />

```javascript
Input: root = [1,2,3]
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
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
var sumNumbers = function (root) {
  //Add root value to next level
  let sum = 0;
  const dfs = (node, val) => {
    if (!node) return;
    //Add current value to next level
    val = val * 10 + node.val;
    //If leaf node, add to sum
    if (!node.left && !node.right) {
      sum += val;
      return;
    }
    dfs(node.left, val);
    dfs(node.right, val);
  };
  dfs(root, 0);
  return sum;
};
```
