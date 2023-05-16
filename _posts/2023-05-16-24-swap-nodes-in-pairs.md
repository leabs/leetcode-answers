---
layout: post
title: 24. Swap Nodes in Pairs
date: 2023-05-16 09:00 -0400
difficulty: medium
comments: true
---

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

## Example

<img src="{{ site.baseurl }}/assets/images/may-16.jpg" alt="Example tree image"  style="max-width:300px" />

```javascript
Input: head = [1, 2, 3, 4];
Output: [2, 1, 4, 3];
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
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function (head) {
  //Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

  let dummy = new ListNode(0);
  dummy.next = head;
  let current = dummy;

  while (current.next !== null && current.next.next !== null) {
    let first = current.next;
    let second = current.next.next;
    first.next = second.next;
    current.next = second;
    current.next.next = first;
    current = current.next.next;
  }

  return dummy.next;
};
```
