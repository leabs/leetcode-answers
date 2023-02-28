---
layout: post
title: 652. Find Duplicate Subtrees
date: 2023-02-28 08:29 -0500
difficulty: medium
comments: true
---

Given the `root` of a binary tree, return all **duplicate subtrees**.

For each kind of duplicate subtrees, you only need to return the root node of any one of them.

Two trees are **duplicate** if they have the same structure with the **same node values**.

## Example

<img src="{{ site.baseurl }}/assets/images/feb-28.jpg" alt="Example tree image" />

```javascript
Input: root = [1, 2, 3, 4, null, 2, 4, null, null, 4];
Output: [[2, 4], [4]];
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
 * @return {TreeNode[]}
 */
var findDuplicateSubtrees = function (root) {
  //Loop through the tree and store the values in a map
  //If the value is already in the map, add it to the result array
  //Return the result array
  let map = new Map();
  let result = [];
  let traverse = (node) => {
    //If the node is null, return a string
    if (!node) return "#";
    let left = traverse(node.left);
    let right = traverse(node.right);
    //Create a key for the map
    let key = `${node.val},${left},${right}`;
    if (map.has(key)) {
      if (map.get(key) === 1) {
        //If the key is already in the map, add it to the result array
        result.push(node);
      }
      //Increment the value of the key
      map.set(key, map.get(key) + 1);
    } else {
      //If the key is not in the map, add it to the map
      map.set(key, 1);
    }
    //Return the key
    return key;
  };
  //Call the traverse function
  traverse(root);
  //Return the result array
  return result;
};
```
