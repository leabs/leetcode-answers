---
layout: post
title: "2130. Maximum Twin Sum of a Linked List"
date: 2023-05-17 08:10 -0400
difficulty: medium
comments: true
---

In a linked list of size `n`, where `n` is even, the `ith` node (0-indexed) of the linked list is known as the twin of the `(n-1-i)th` node, if `0 <= i <= (n / 2) - 1`.

- For example, if `n = 4`, then node `0` is the twin of node `3`, and node `1` is the twin of node `2`. These are the only nodes with twins for `n = 4`.

The twin sum is defined as the sum of a node and its twin.

Given the `head` of a linked list with even length, return the maximum twin sum of the linked list.

## Example

<img src="{{ site.baseurl }}/assets/images/may-17.png" alt="Example tree image"  style="max-width:300px" />

```javascript
Input: head = [5,4,2,1]
Output: 6
Explanation:
Nodes 0 and 1 are the twins of nodes 3 and 2, respectively. All have twin sum = 6.
There are no other nodes with twins in the linked list.
Thus, the maximum twin sum of the linked list is 6.
```

## Solution

Great solution found [here](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/solutions/1728750/beginner-friendly-java-javascript-python-solution/)

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
 * @return {number}
 */
var pairSum = function (head) {
  //Set st to an empty array
  var st = [];
  //While head is not empty
  while (head != null) {
    //Add head.val to st
    st.push(head.val);
    //Set head to head.next
    head = head.next;
  }
  //Set max
  let max = 0;
  //For each number in st
  for (let i = 0; i < st.length; i++) {
    //Set max to the max of max and st[i] + st[st.length-1-i]
    max = Math.max(max, st[i] + st[st.length - 1 - i]);
  }
  return max;
};
```
