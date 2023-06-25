---
layout: post
title: 1575. Count All Possible Routes
date: 2023-06-25 11:05 -0400
difficulty:
comments: true
---

You are given an array of distinct positive integers locations where `locations[i]` represents the position of city `i`. You are also given integers `start`, `finish` and `fuel` representing the starting city, ending city, and the initial amount of fuel you have, respectively.

At each step, if you are at city `i`, you can pick any city `j` such that `j != i` and `0 <= j < locations.length` and move to city `j`. Moving from city `i` to city `j` reduces the amount of fuel you have by `|locations[i] - locations[j]|`. Please notice that `|x|` denotes the absolute value of `x`.

Notice that `fuel` **cannot** become negative at any point in time, and that you are allowed to visit any city more than once (including `start` and `finish`).

Return the count of all possible routes from `start` to `finish`. Since the answer may be too large, return it modulo `109 + 7`.

## Example

```javascript
Input: locations = [2,3,6,8,4], start = 1, finish = 3, fuel = 5
Output: 4
Explanation: The following are all possible routes, each uses 5 units of fuel:
1 -> 3
1 -> 2 -> 3
1 -> 4 -> 3
1 -> 4 -> 2 -> 3
```

## Solution

Great solution [here](https://leetcode.com/problems/count-all-possible-routes/solutions/3680421/easy-to-read-javascript-solution-w-explanation/)

```javascript
var countRoutes = function (locations, start, finish, fuel) {
  // Map to keep track of visited nodes and paths to end with those conditions
  let visited = new Map();

  // Modulo to use
  let mod = 10 ** 9 + 7;

  // DFS function
  let dfs = (current, fuel) => {
    // Generate a key in the "2D" memo matrix
    let id = `${current},${fuel}`;

    // If we haven't visited already...
    if (!visited.has(id)) {
      let paths = 0;
      // Count the paths; if we already finished, increment paths
      if (current === finish) paths++;
      // Go through all other positions...
      for (let i = 0; i < locations.length; i++) {
        if (i !== current) {
          // Calculate remaining fuel
          let remaining = fuel - Math.abs(locations[current] - locations[i]);
          // If sufficient fuel, DFS further from current position
          if (remaining >= 0) {
            paths += dfs(i, remaining);
          }
        }
      }
      visited.set(id, paths % mod);
    }

    // Finally, cache result
    return visited.get(id);
  };

  // Run DFS on starting node
  return dfs(start, fuel);
};
```
