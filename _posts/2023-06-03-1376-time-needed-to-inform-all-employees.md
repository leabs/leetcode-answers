---
layout: post
title: 1376. Time Needed to Inform All Employees
date: 2023-06-03 08:39 -0400
difficulty: medium
comments: true
---

A company has `n` employees with a unique ID for each employee from `0` to `n - 1`. The head of the company is the one with headID.

Each employee has one direct manager given in the `manager` array where `manager[i]` is the direct manager of the `i-th` employee, `manager[headID] = -1`. Also, it is guaranteed that the subordination relationships have a tree structure.

The head of the company wants to inform all the company employees of an urgent piece of news. He will inform his direct subordinates, and they will inform their subordinates, and so on until all employees know about the urgent news.

The `i-th` employee needs `informTime[i]` minutes to inform all of his direct subordinates (i.e., After informTime[i] minutes, all his direct subordinates can start spreading the news).

Return the number of minutes needed to inform all the employees about the urgent news.

## Example

```javascript
Input: n = 1, headID = 0, manager = [-1], informTime = [0]
Output: 0
Explanation: The head of the company is the only employee in the company.
```

## Solution

```javascript
/**
 * @param {number} n
 * @param {number} headID
 * @param {number[]} manager
 * @param {number[]} informTime
 * @return {number}
 */
var numOfMinutes = function (n, headID, manager, informTime) {
  //Declare a map to store the manager and its subordinates
  const map = new Map();
  for (let i = 0; i < n; i++) {
    //If the manager is -1, it means it is the head
    if (manager[i] === -1) continue;
    //If the manager is not in the map, add it
    if (!map.has(manager[i])) map.set(manager[i], []);
    //Add the subordinate to the manager
    map.get(manager[i]).push(i);
  }

  const dfs = (id, time) => {
    //If the manager is not in the map, return the time
    if (!map.has(id)) return time;
    let max = 0;
    for (let i = 0; i < map.get(id).length; i++) {
      //Find the max time
      max = Math.max(max, dfs(map.get(id)[i], time + informTime[id]));
    }
    return max;
  };
  return dfs(headID, 0);
};
```
