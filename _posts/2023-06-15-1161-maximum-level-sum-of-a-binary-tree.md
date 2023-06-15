---
layout: post
title: 1161. Maximum Level Sum of a Binary Tree
date: 2023-06-15 07:58 -0400
difficulty: medium
comments: true
---

Given the `root` of a binary tree, the level of its `root` is `1`, the level of its children is `2`, and so on.

Return the smallest level `x` such that the sum of all the values of nodes at level `x` is maximal.

## Example

<img src="{{ site.baseurl }}/assets/images/jun-15.jpeg" alt="example tree image" width="300"/>

```javascript
Input: root = [1,7,0,7,-8,null,null]
Output: 2
Explanation:
Level 1 sum = 1.
Level 2 sum = 7 + 0 = 7.
Level 3 sum = 7 + -8 = -1.
So we return the level with the maximum sum which is level 2.
```

## Solution

Great solution [here](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/solutions/472665/javascript-bfs-iterative-one-queue/)

```javascript
var maxLevelSum = function (root) {
  //if no root, return 1
  if (!root) return 1;

  //Declare queue and levels array
  const queue = [root];
  const levels = [];

  //while queue is not empty
  while (queue.length) {
    //declare level array and size variable
    const level = [];
    let size = queue.length;

    //loop through queue
    for (let i = 0; i < size; i++) {
      //shift node from queue
      const node = queue.shift();
      //push node value to level array
      level.push(node.val);

      //if node has children, push them to queue
      if (node.left) queue.push(node.left);
      //if node has children, push them to queue
      if (node.right) queue.push(node.right);
    }
    //push sum of level to levels array
    levels.push(level.reduce((acc, curr) => acc + curr));
  }
  //return index of max value in levels array + 1
  return levels.indexOf(Math.max(...levels)) + 1;
};
```
