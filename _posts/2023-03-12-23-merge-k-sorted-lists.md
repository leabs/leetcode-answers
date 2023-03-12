---
layout: post
title: 23. Merge k Sorted Lists
date: 2023-03-12 08:59 -0400
difficulty: hard
comments: true
---

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

## Example

```javascript
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

## Solution

Great solution [here](https://leetcode.com/problems/merge-k-sorted-lists/solutions/114606/extremely-simple-javascript-solution/?orderBy=hot&languageTags=javascript).

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
function mergeLists(a, b) {
  const dummy = new ListNode(0);
  let temp = dummy;
  //While lists are not empty
  while (a !== null && b !== null) {
    if (a.val < b.val) {
      //If a is less than b, add a to the list
      temp.next = a;
      a = a.next;
    } else {
      //If b is less than a, add b to the list
      temp.next = b;
      b = b.next;
    }
    temp = temp.next;
  }
  if (a !== null) {
    temp.next = a;
  }
  if (b !== null) {
    temp.next = b;
  }
  return dummy.next;
}

var mergeKLists = function (lists) {
  if (lists.length === 0) {
    return null;
  }
  // two two
  // priority queue
  while (lists.length > 1) {
    // the head will contains the "less" length list
    let a = lists.shift();
    // acturally, we can use the linkedlist to replace it, the while loop will be the while( list.header.next !== null || lists.length > 0)
    let b = lists.shift();
    const h = mergeLists(a, b);
    lists.push(h);
  }
  return lists[0];
};
```
