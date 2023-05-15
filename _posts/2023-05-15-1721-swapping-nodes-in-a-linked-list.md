---
layout: post
title: 1721. Swapping Nodes in a Linked List
date: 2023-05-15 08:39 -0400
difficulty: medium
comments: true
---

You are given the `head` of a linked list, and an integer `k`.

Return the head of the linked list after **swapping** the values of the kth node from the beginning and the `kth` node from the end (the list is **1-indexed**).

## Example

<img src="{{ site.baseurl }}/assets/images/may-15.png" alt="Example tree image"  style="max-width:300px" />

```javascript
Input: (head = [1, 2, 3, 4, 5]), (k = 2);
Output: [1, 4, 3, 2, 5];
```

## Solution

Great solution found [here](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/solutions/1912048/beginner-friendly-javascript-solution/?languageTags=javascript)

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var swapNodes = function (head, k) {
  //Set fast, second, and first to head
  let fast = head,
    second = head,
    first = head;
  //For k - 1 times
  for (let i = 0; i < k - 1; i++) {
    fast = fast.next;
  }
  first = fast;
  while (fast.next != null) {
    fast = fast.next;
    second = second.next;
  }
  let temp = first.val;
  first.val = second.val;
  second.val = temp;
  return head;
};
```
