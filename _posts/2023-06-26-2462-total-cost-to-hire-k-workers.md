---
layout: post
title: 2462. Total Cost to Hire K Workers
date: 2023-06-26 07:50 -0400
difficulty: medium
comments: true
---

You are given a 0-indexed integer array `costs` where `costs[i]` is the cost of hiring the `ith` worker.

You are also given two integers `k` and `candidates`. We want to hire exactly `k` workers according to the following rules:

- You will run `k` sessions and hire exactly one worker in each session.
- In each hiring session, choose the worker with the lowest cost from either the first candidates workers or the last candidates workers. Break the tie by the smallest index.
  - For example, if `costs = [3,2,7,7,1,2]` and `candidates = 2`, then in the first hiring session, we will choose the 4th worker because they have the lowest cost `[3,2,7,7,1,2]`.
  - In the second hiring session, we will choose 1st worker because they have the same lowest cost as 4th worker but they have the smallest index `[3,2,7,7,2]`. Please note that the indexing may be changed in the process.
- If there are fewer than candidates workers remaining, choose the worker with the lowest cost among them. Break the tie by the smallest index.
- A worker can only be chosen once.

Return the total cost to hire exactly `k` workers.

## Example

```javascript
Input: costs = [17,12,10,2,7,2,11,20,8], k = 3, candidates = 4
Output: 11
Explanation: We hire 3 workers in total. The total cost is initially 0.
- In the first hiring round we choose the worker from [17,12,10,2,7,2,11,20,8]. The lowest cost is 2, and we break the tie by the smallest index, which is 3. The total cost = 0 + 2 = 2.
- In the second hiring round we choose the worker from [17,12,10,7,2,11,20,8]. The lowest cost is 2 (index 4). The total cost = 2 + 2 = 4.
- In the third hiring round we choose the worker from [17,12,10,7,11,20,8]. The lowest cost is 7 (index 3). The total cost = 4 + 7 = 11. Notice that the worker with index 3 was common in the first and last four workers.
The total hiring cost is 11.
```

## Solution

Great solution found [here](https://leetcode.com/problems/total-cost-to-hire-k-workers/solutions/2783439/javascript-min-heap-pq-476ms/)

```javascript
const totalCost = (a, k, m) => {
  // create a min heap that stores the minimum value along with its index
  let pq = new MinPriorityQueue({
    compare: (x, y) => {
      if (x[0] != y[0]) return x[0] - y[0];
      return x[1] - y[1];
    },
  });

  // initialize the left and right pointers
  let n = a.length,
    l = 0,
    r = n - 1,
    res = 0;

  // add the first m elements to the heap
  for (let i = 0; i < m; i++) {
    if (l <= r) {
      pq.enqueue([a[l], l]);
      l++;
    }
  }

  // add the last m elements to the heap
  for (let i = 0; i < m; i++) {
    if (l <= r) {
      pq.enqueue([a[r], r]);
      r--;
    }
  }

  // iterate k times, removing the smallest element and adding the next one
  for (let i = 0; i < k; i++) {
    let cur = pq.dequeue();
    res += cur[0];
    if (cur[1] < l && l <= r) {
      pq.enqueue([a[l], l]);
      l++;
    } else if (cur[1] > r && l <= r) {
      pq.enqueue([a[r], r]);
      r--;
    }
  }
  return res;
};
```
