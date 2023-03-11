---
layout: post
title: 109. Convert Sorted List to Binary Search Tree
date: 2023-03-11 08:04 -0500
difficulty: medium
comments: true
---

Given the `head` of a singly linked list where elements are sorted in **ascending order**, convert it to a
height-balanced binary search tree.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-11.png" alt="Example tree image" />

```javascript
Input: head = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.
```

## Solution

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {ListNode} head
 * @return {TreeNode}
 */
var sortedListToBST = function (head) {
  // If head is empty return null
  if (!head) return null;
  // If head.next is empty return new TreeNode with head.val
  if (!head.next) return new TreeNode(head.val);

  let slow = head;
  let fast = head;
  let prev = null;

  while (fast && fast.next) {
    fast = fast.next.next;
    prev = slow;
    slow = slow.next;
  }

  prev.next = null;

  // Create new TreeNode with slow.val
  let root = new TreeNode(slow.val);
  root.left = sortedListToBST(head);
  root.right = sortedListToBST(slow.next);

  return root;
};
```
