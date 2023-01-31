---
layout: post
title: 1626. Best Team With No Conflicts
date: 2023-01-31 08:12 -0500
difficulty: medium
comments: true
---

You are the manager of a basketball team. For the upcoming tournament, you want to choose the team with the highest overall score. The score of the team is the sum of scores of all the players in the team.

However, the basketball team is not allowed to have **conflicts**. A **conflict** exists if a younger player has **a strictly higher** score than an older player. A conflict does not occur between players of the same age.

Given two lists, `scores` and `ages`, where each `scores[i]` and `ages[i]` represents the score and age of the `ith` player, respectively, return the _highest overall score of all possible basketball teams_.

## Example:

<pre><strong>Input:</strong> scores = [1,3,5,10,15], ages = [1,2,3,4,5]
<strong>Output:</strong> 34
<strong>Explanation:</strong>&nbsp;You can choose all the players.
</pre>

```javascript
/**
 * @param {number[]} scores
 * @param {number[]} ages
 * @return {number}
 */
var bestTeamScore = function (scores, ages) {
  //Declare an empty array
  let arr = [];

  //Push the ages and scores of each player into the array
  for (let i = 0; i < scores.length; i++) {
    arr.push([ages[i], scores[i]]);
  }
  //Sort the array by age and score
  arr.sort((a, b) => (a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]));

  // Declare an array of size scores.length and fill it with 0
  let res = new Array(scores.length).fill(0);
  res[0] = arr[0][1];

  //Loop through the array
  for (let i = 1; i < arr.length; i++) {
    //Declare variables for the age and score of the ith player
    let [fa, fs] = arr[i];
    //The score of the ith player is the score of the ith player
    res[i] = fs;
    //Loop through the array backwards
    for (let j = i - 1; j >= 0; j--) {
      //Declare variables for the age and score of the jth player
      let [sa, ss] = arr[j];
      //If the age of the ith player is greater than the age of the jth player
      if (sa == fa) res[i] = Math.max(res[i], res[j] + fs);
      else {
        if (fs >= ss) {
          //The score of the ith player is the maximum of the score of the ith player and the score of the jth player plus the score of the ith player
          res[i] = Math.max(res[i], res[j] + fs);
        }
      }
    }
  }
  //Return the maximum score
  return Math.max(...res);
};
```
