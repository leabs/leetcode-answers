---
layout: post
title: 1402. Reducing Dishes
date: 2023-03-29 08:17 -0400
difficulty: hard
comments: true
---

A chef has collected data on the `satisfaction` level of his `n` dishes. Chef can cook any dish in 1 unit of time.

Like-time coefficient of a dish is defined as the time taken to cook that dish including previous dishes multiplied by its satisfaction level i.e. `time[i] * satisfaction[i]`.

Return the maximum sum of **like-time** coefficient that the chef can obtain after dishes preparation.

Dishes can be prepared in any order and the chef can discard some dishes to get this maximum value.

## Example

```javascript
Input: satisfaction = [-1,-8,0,5,-9]
Output: 14
Explanation: After Removing the second and last dish, the maximum total like-time coefficient will be equal to (-1*1 + 0*2 + 5*3 = 14).
Each dish is prepared in one unit of time.
```

## Solution

```javascript
/**
 * Return the maximum sum of **like-time** coefficient that the chef can obtain after dishes preparation
 * @param {number[]} satisfaction
 * @return {number}
 */
var maxSatisfaction = function (satisfaction) {
  //Sort the dishes in descending order
  satisfaction.sort((a, b) => b - a);
  let sum = 0;
  let max = 0;
  //Loop through the dishes
  for (let i = 0; i < satisfaction.length; i++) {
    //Add the current dish's satisfaction to the sum
    sum += satisfaction[i];
    //If the sum is less than 0, break out of the loop
    if (sum < 0) {
      break;
    }
    //Add the sum to the max
    max += sum;
  }
  return max;
};
```
