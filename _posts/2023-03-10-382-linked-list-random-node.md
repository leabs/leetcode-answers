---
layout: post
title: 382. Linked List Random Node
date: 2023-03-10 07:47 -0500
difficulty: medium
comments: true
---

Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

Implement the `Solution` class:

- Solution(ListNode head) Initializes the object with the head of the singly-linked list head.
- int getRandom() Chooses a node randomly from the list and returns its value. All the nodes of the list should be equally likely to be chosen.

## Example

```javascript
Input
["Solution", "getRandom", "getRandom", "getRandom", "getRandom", "getRandom"]
[[[1, 2, 3]], [], [], [], [], []]
Output
[null, 1, 3, 2, 2, 3]

Explanation
Solution solution = new Solution([1, 2, 3]);
solution.getRandom(); // return 1
solution.getRandom(); // return 3
solution.getRandom(); // return 2
solution.getRandom(); // return 2
solution.getRandom(); // return 3
// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
```

## Solution

Great solution [here](https://leetcode.com/problems/linked-list-random-node/solutions/3280143/fast-and-easy-solution/?orderBy=hot&languageTags=javascript).

```javascript
/**
 * @param {ListNode} head
 */
var Solution = function(head) {
    // Create a list to store all the values
    this.list = [];
    // While head is not null
    while(head){
        // Push the value of the node into the list
        this.list.push(head.val);
        // Move to the next node
        head = head.next;
    }
};

/**
 * @return {number}
 */
Solution.prototype.getRandom = function() {
    // Return a random value from the list
    return this.list[Math.floor(Math.random() * this.list.length)];
};
```
