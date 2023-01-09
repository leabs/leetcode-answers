---
layout: post
title: "144. Binary Tree Preorder Traversal"
date: 2023-01-09 10:35:33 -0500
comments: true
---
Given the `root` of a binary tree, return the *preorder traversal of its nodes' values*.

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
 * @return {number[]}
 */
var preorderTraversal = function (root) {
  //Return an empty array if root is null
    if (root === null) {
        return [];
    }
    //Create a result array
    let result = [];
    //Create a stack
    let stack = [];
    //Push root to stack
    stack.push(root);
    //WHILE stack is not empty
    while (stack.length !== 0) {
        //Set current to stack.pop()
        let current = stack.pop();
        //Push current.val to result
        result.push(current.val);
        //IF current.right is not null
        if (current.right !== null) {
            //Push current.right to stack
            stack.push(current.right);
        }
        //IF current.left is not null
        if (current.left !== null) {
            //Push current.left to stack
            stack.push(current.left);
        }
    }
    //Return result
    return result;
};

```