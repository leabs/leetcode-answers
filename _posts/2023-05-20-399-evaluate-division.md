---
layout: post
title: 399. Evaluate Division
date: 2023-05-20 09:29 -0400
difficulty: medium
comments: true
---

You are given an array of variable pairs `equations` and an array of real numbers `values`, where `equations[i] = [Ai, Bi]` and `values[i]` represent the equation `Ai / Bi = values[i]`. Each Ai or Bi is a string that represents a single variable.

You are also given some `queries`, where` queries[j] = [Cj, Dj]` represents the `jth` query where you must find the answer for `Cj / Dj = ?`.

Return the answers to all queries. If a single answer cannot be determined, return `-1.0`.

Note: The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

## Example

```javascript
Input: equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
Explanation:
Given: a / b = 2.0, b / c = 3.0
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]
```

## Solution

```javascript
/**
 * @param {string[][]} equations
 * @param {number[]} values
 * @param {string[][]} queries
 * @return {number[]}
 */
var calcEquation = function (equations, values, queries) {
  //Create a graph
  const graph = {};
  //Loop through equations
  for (let i = 0; i < equations.length; i++) {
    //Set the first variable to the first element of the equation
    const [first] = equations[i];
    //Set the second variable to the second element of the equation
    const [, second] = equations[i];
    //If the first variable is not in the graph, set it to an empty object
    if (!graph[first]) graph[first] = {};
    //If the second variable is not in the graph, set it to an empty object
    if (!graph[second]) graph[second] = {};
    //Set the first variable to the second variable with the value of the equation
    graph[first][second] = values[i];
    //Set the second variable to the first variable with the value of the equation
    graph[second][first] = 1 / values[i];
  }
  //Create a function to find the value of the query
  const findValue = (first, second, visited = new Set()) => {
    //If the first variable is not in the graph, return -1
    if (!graph[first]) return -1;
    //If the second variable is not in the graph, return -1
    if (!graph[second]) return -1;
    //If the first variable is the same as the second variable, return 1
    if (first === second) return 1;
    //If the second variable is in the first variable, return the value of the equation
    if (graph[first][second]) return graph[first][second];
    //Add the first variable to the visited set
    visited.add(first);
    //Loop through the keys of the first variable
    for (const key of Object.keys(graph[first])) {
      //If the visited set does not have the key, set the value of the equation to the value of the equation times the value of the key
      if (!visited.has(key)) {
        const value = findValue(key, second, visited);
        if (value !== -1) return graph[first][key] * value;
      }
    }
    //Return -1
    return -1;
  };
  //Create an array to store the answers
  const answers = [];
  //Loop through the queries
  for (let i = 0; i < queries.length; i++) {
    //Set the first variable to the first element of the query
    const [first] = queries[i];
    //Set the second variable to the second element of the query
    const [, second] = queries[i];
    //Push the value of the query to the answers array
    answers.push(findValue(first, second));
  }
  //Return the answers array
  return answers;
};
```
