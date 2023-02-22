---
layout: post
title: "2246. Longest Path With Different Adjacent Characters"
date: 2023-01-13 07:35:33 -0500
comments: true
difficulty: hard
---

You are given a tree (i.e. a connected, undirected graph that has no cycles) rooted at node 0 consisting of n nodes numbered from 0 to n - 1. The tree is represented by a 0-indexed array parent of size n, where parent[i] is the parent of node i. Since node 0 is the root, parent[0] == -1.

You are also given a string s of length n, where s[i] is the character assigned to node i.

Return the length of the longest path in the tree such that no pair of adjacent nodes on the path have the same character assigned to them.

<pre><strong>Input:</strong> parent = [-1,0,0,1,1,2], s = "abacbe"
<strong>Output:</strong> 3
<strong>Explanation:</strong> The longest path where each two adjacent nodes have different characters in the tree is the path: 0 -&gt; 1 -&gt; 3. The length of this path is 3, so 3 is returned.
It can be proven that there is no longer path that satisfies the conditions. 
</pre>

## Solution

```javascript
/**
 * @param {number[]} parent
 * @param {string} s
 * @return {number}
 */

//Find the longest path in the tree such that no pair of adjacent nodes on the path have the same character assigned to them.
var longestPath = function (parent, s) {
  //Set n to the length of the parent array
  let n = parent.length;
  //Initialize the children array
  let children = new Array(n);
  //Loop through the parent array
  for (let i = 0; i < n; i++) {
    children[i] = new Array();
  }
  //Push the children of each node into the children array
  for (let i = 1; i < n; i++) {
    children[parent[i]].push(i);
  }
  //Split the string into an array of characters
  s = s.split("");
  //Initialize the longest path to 0
  let longestPath = 0;
  //Initialize the dfs function
  let dfs = function (node) {
    let longestLength = 0,
      longestLength2 = 0;
    //Loop through the children of each node
    for (let child of children[node]) {
      let lengthChild = dfs(child);
      //If the character of the node is the same as the character of the child, continue
      if (s[node] == s[child]) continue;
      //If the length of the child is greater than the longest length, set the longest length to the length of the child
      if (longestLength < lengthChild) {
        longestLength2 = longestLength;
        longestLength = lengthChild;
      }
      //If the length of the child is greater than the second longest length, set the second longest length to the length of the child
      else if (longestLength2 < lengthChild) {
        longestLength2 = lengthChild;
      }
    }
    //Set the longest path to the longest length plus the second longest length plus 1
    longestPath = Math.max(longestPath, longestLength + longestLength2 + 1);
    //Return the longest length plus 1
    return longestLength + 1;
  };
  //Call the dfs function
  dfs(0);
  //Return the longest path
  return longestPath;
};
```
