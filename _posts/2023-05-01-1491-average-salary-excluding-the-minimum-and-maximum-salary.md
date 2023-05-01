---
layout: post
title: 1491. Average Salary Excluding the Minimum and Maximum Salary
date: 2023-05-01 07:54 -0400
difficulty: easy
comments: true
---

You are given an array of unique integers `salary` where `salary[i]` is the salary of the ith employee.

Return the average salary of employees excluding the minimum and maximum salary. Answers within 10-5 of the actual answer will be accepted.

## Example

```javascript
Input: salary = [4000,3000,1000,2000]
Output: 2500.00000
Explanation: Minimum salary and maximum salary are 1000 and 4000 respectively.
Average salary excluding minimum and maximum salary is (2000+3000) / 2 = 2500
```

## Solution

```javascript
/**
 * @param {number[]} salary
 * @return {number}
 */
var average = function (salary) {
  //remove the highest number from the salary array
  salary.splice(salary.indexOf(Math.max(...salary)), 1);
  //remove the lowest number from the salary array
  salary.splice(salary.indexOf(Math.min(...salary)), 1);
  //declare sum as 0 to start
  let sum = 0;
  //FOR loop using salary length
  for (let i = 0; i < salary.length; i++) {
    //Add current index to sum
    sum += salary[i];
  }
  //Return sum divided by salary length
  return sum / salary.length;
};
```
