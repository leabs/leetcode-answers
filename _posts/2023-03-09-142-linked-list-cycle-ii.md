---
layout: post
title: 142. Linked List Cycle II
date: 2023-03-09 07:36 -0500
difficulty: medium
comments: true
---

Given the `head` of a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to **(0-indexed)**. It is `-1` if there is no cycle. **Note that** `pos` **is not passed as a parameter**.

**Do not modify** the linked list.

## Example

<img src="{{ site.baseurl }}/assets/images/mar-9.png" alt="Example tree image" />

```javascript
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

## Solution

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var detectCycle = function (head) {
  // If head is empty return null
  if (!head) return null;
  if (!head.next) return null;

  // Set slow and fast to head
  let slow = head;
  let fast = head;
  let pointer = head;

  // While fast and fast.next are not null
  while (fast && fast.next) {
    fast = fast.next.next;
    slow = slow.next;
    if (fast === slow) break;
  }

  if (fast !== slow) return null;

  while (pointer !== slow) {
    pointer = pointer.next;
    slow = slow.next;
  }

  return slow;
};

```
