---
layout: post
title: "491. Non-decreasing Subsequences"
date: 2023-01-20 07:35:33 -0500
comments: true
difficulty: medium
---

Given an integer array `nums`, return _all the different possible non-decreasing subsequences of the given array with at least two elements_. You may return the answer in _any order_.

<pre><strong>Input:</strong> nums = [4,6,7,7]
<strong>Output:</strong> [[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
</pre>

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var findSubsequences = function (nums) {
  // Set to store the result
  let res = [];
  // Map to store the visited elements
  let map = {};
  // Function to iterate through the array
  let iterate = (index, temp) => {
    // If the element is already visited, return
    if (map[temp]) return;
    // If the length of the temp array is greater than 1, push it to the result
    if (temp.length >= 2) {
      // Push the temp array to the result
      res.push(temp);
    }
    // Iterate through the array
    for (let i = index; i < nums.length; i++) {
      // If the last element of the temp array is greater than the current element, continue
      if (temp[temp.length - 1] > nums[i]) continue;
      map[temp] = true;
      // Recursively call the function
      iterate(i + 1, [...temp, nums[i]]);
    }
  };
  // Call the function
  iterate(0, []);
  // Return the result
  return res;
};
```
