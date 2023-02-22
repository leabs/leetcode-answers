---
layout: post
title: 103. Binary Tree Zigzag Level Order Traversal
date: 2023-02-19 07:14 -0500
difficulty: medium
comments: true
---

Given the `root` of a binary tree, return the _zigzag level order traversal of its nodes' values._ (i.e., from left to right, then right to left for the next level and alternate between).

```javascript
Input: root = [3, 9, 20, null, null, 15, 7];
Output: [[3], [20, 9], [15, 7]];
```

Great solution [here.](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/solutions/3122259/simple-soln-in-js/?orderBy=hot&languageTags=javascript)

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
 * @return {number[][]}
 */
 
var zigzagLevelOrder = function(root) {
    //If root is null, return empty array.
    if(root == null) return [];

    let q = [];
    let ans = [];

    let leftToRight = true;
    q.push(root);

    while(q.length != 0){
        let levelNodesList = [];
        //Get the number of nodes at the current level.
        let nodesAtCurrlevel = q.length;

        //Iterate through the nodes at the current level.
        for(let i = nodesAtCurrlevel; i>0; i--){
            let currNode = q.shift();

            if(leftToRight == true){
                levelNodesList.push(currNode.val);
            }else{
                levelNodesList.unshift(currNode.val);
            }

            if(currNode.left != null){
                q.push(currNode.left)
            }

            if(currNode.right != null){
                q.push(currNode.right)
            }
        }

        leftToRight = !leftToRight;
        //Add the nodes at the current level to the answer.
        ans.push(levelNodesList);
    }
    //Return the answer.
    return ans;
};
```
