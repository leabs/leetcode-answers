---
layout: post
title: 2140. Solving Questions With Brainpower
date: 2023-05-12 07:59 -0400
difficulty: medium
comments: true
---

You are given a 0-indexed 2D integer array `questions` where `questions[i]` = `[pointsi, brainpoweri]`.

The array describes the questions of an exam, where you have to process the questions in order (i.e., starting from question 0) and make a decision whether to solve or skip each question. Solving question i will earn you pointsi points but you will be unable to solve each of the next brainpoweri questions. If you skip question i, you get to make the decision on the next question.

For example, given `questions = [[3, 2], [4, 3], [4, 4], [2, 5]]`:

- If question 0 is solved, you will earn 3 points but you will be unable to solve questions 1 and 2.
- If instead, question 0 is skipped and question 1 is solved, you will earn 4 points but you will be unable to solve questions 2 and 3.

Return the **maximum** points you can earn for the exam.

## Example

```javascript
Input: questions = [[3,2],[4,3],[4,4],[2,5]]
Output: 5
Explanation: The maximum points can be earned by solving questions 0 and 3.
- Solve question 0: Earn 3 points, will be unable to solve the next 2 questions
- Unable to solve questions 1 and 2
- Solve question 3: Earn 2 points
Total points earned: 3 + 2 = 5. There is no other way to earn 5 or more points.
```

## Solution

Great solution found [here](https://leetcode.com/problems/solving-questions-with-brainpower/solutions/1696021/beginner-friendly-solutions-from-recursive-memoization-to-iterative-js-easy-o-n/?orderBy=most_votes&languageTags=javascript)

```javascript
/**
 * @param {number[][]} questions
 * @return {number}
 */
var mostPoints = function (questions) {
  // Set up a variable for the total number of questions
  let totalQuestions = questions.length;
  // Set up a variable for the total number of points
  let dp = new Array(totalQuestions).fill(0);
  //FOR LOOP: Loop through the questions array
  for (let i = totalQuestions - 1; i >= 0; i--) {
    // Set up a variable for the current question
    let point = questions[i][0];
    // Set up a variable for the current question's brainpower
    let power = questions[i][1];

    // Set up a variable for the total number of points
    let solve = point + (dp[i + power + 1] || 0);
    // Set up a variable for skipped questions
    let skip = dp[i + 1] || 0;

    //Solve for the maximum number of points
    dp[i] = Math.max(solve, skip);
  }
  return dp[0];
};
```
