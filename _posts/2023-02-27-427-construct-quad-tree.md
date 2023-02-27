---
layout: post
title: 427. Construct Quad Tree
date: 2023-02-27 08:06 -0500
difficulty: medium
comments: true
---

Given a `n \* n` matrix `grid` of `0's` and `1's` only. We want to represent the grid with a Quad-Tree.

Return the root of the Quad-Tree representing the `grid`.

Notice that you can assign the value of a node to True or False when `isLeaf` is **False**, and both are **accepted** in the answer.

A Quad-Tree is a tree data structure in which each internal node has exactly four children. Besides, each node has two attributes:

- `val`: True if the node represents a grid of 1's or False if the node represents a grid of 0's.
- `isLeaf`: True if the node is leaf node on the tree or False if the node has the four children.

```javascript
class Node {
    public boolean val;
    public boolean isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;
}
```

We can construct a Quad-Tree from a two-dimensional area using the following steps:

If the current grid has the same value (i.e all `1's` or all `0's`) set `isLeaf` True and set `val` to the value of the grid and set the four children to Null and stop.

If the current grid has different values, set `isLeaf` to False and set `val` to any value and divide the current grid into four sub-grids as shown in the photo.

Recurse for each of the children with the proper sub-grid.

<img src="{{ site.baseurl }}/assets/images/feb-27-1.png" alt="Example grid image" />
If you want to know more about the Quad-Tree, you can refer to the [wiki](https://en.wikipedia.org/wiki/Quadtree).

### Quad-Tree format

The output represents the serialized format of a Quad-Tree using level order traversal, where `null` signifies a path terminator where no node exists below.

It is very similar to the serialization of the binary tree. The only difference is that the node is represented as a list `[isLeaf, val]`.

If the value of `isLeaf` or `val` is True we represent it as 1 in the list `[isLeaf, val]` and if the value of `isLeaf` or `val` is False we represent it as 0.

## Example

<img src="{{ site.baseurl }}/assets/images/feb-27-2.png" alt="Example grid image" />

```javascript
Input: grid = [[0,1],[1,0]]
Output: [[0,1],[1,0],[1,1],[1,1],[1,0]]
Explanation: The explanation of this example is shown below:
Notice that 0 represnts False and 1 represents True in the photo representing the Quad-Tree.
```

## Solution

I found a nice working solution [here](https://leetcode.com/problems/construct-quad-tree/solutions/3236091/easy-solution/?orderBy=hot&languageTags=javascript) with a great write up!.

```javascript
/**
 * // Definition for a QuadTree node.
 * function Node(val,isLeaf,topLeft,topRight,bottomLeft,bottomRight) {
 *    this.val = val;
 *    this.isLeaf = isLeaf;
 *    this.topLeft = topLeft;
 *    this.topRight = topRight;
 *    this.bottomLeft = bottomLeft;
 *    this.bottomRight = bottomRight;
 * };
 */

/**
 * @param {number[][]} grid
 * @return {Node}
 */
let construct_helper = (grid, n, startR, endR, startC, endC) => {
  if (n == 1) {
    //return new node with val = grid[startR][startC] and isLeaf = true
    return new Node(grid[startR][startC], 1);
  }
  let curr = new Node(1, 1);
  let upper_left = construct_helper(
    grid,
    n / 2,
    startR,
    startR - 1 + n / 2,
    startC,
    startC - 1 + n / 2
  );
  let upper_right = construct_helper(
    grid,
    n / 2,
    startR,
    startR - 1 + n / 2,
    startC + n / 2,
    endC
  );
  let lower_left = construct_helper(
    grid,
    n / 2,
    startR + n / 2,
    endR,
    startC,
    startC - 1 + n / 2
  );
  let lower_right = construct_helper(
    grid,
    n / 2,
    startR + n / 2,
    endR,
    startC + n / 2,
    endC
  );
  if (
    upper_left.val == lower_left.val &&
    upper_left.val == upper_right.val &&
    upper_left.val == lower_right.val &&
    upper_left.isLeaf &&
    upper_right.isLeaf &&
    lower_left.isLeaf &&
    lower_right.isLeaf
  ) {
    curr.val = upper_left.val;
  } else {
    curr.isLeaf = 0;
    curr.topLeft = upper_left;
    curr.topRight = upper_right;
    curr.bottomLeft = lower_left;
    curr.bottomRight = lower_right;
  }

  return curr;
};
var construct = function (grid) {
  return construct_helper(
    grid,
    grid.length,
    0,
    grid.length - 1,
    0,
    grid.length - 1
  );
};
```
