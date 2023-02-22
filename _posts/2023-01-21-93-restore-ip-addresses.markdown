---
layout: post
title: "93. Restore IP Addresses"
date: 2023-01-21 07:35:33 -0500
comments: true
difficulty: medium
---

A valid IP address consists of exactly four integers separated by single dots. Each integer is between `0` and `255` **(inclusive)** and cannot have leading zeros.

- For example, `"0.1.2.201"` and `"192.168.1.1"` are **valid** IP addresses, but `"0.011.255.245"`, `"192.168.1.312"` and `"192.168@1.1"` are invalid IP addresses.

Given a string `s` containing only digits, return _all possible valid IP addresses that can be formed by inserting dots into_ `s`. You are **not** allowed to reorder or remove any digits in `s`. You may return the valid IP addresses in **any** order.

<pre><strong>Input:</strong> s = "25525511135"
<strong>Output:</strong> ["255.255.11.135","255.255.111.35"]
</pre>

## Solution

```javascript
/**
 * @param {string} s
 * @return {string[]}
 */
var restoreIpAddresses = function (s) {
  //
  if (s.length > 12 || s.length < 4) return [];
  // Result array
  let res = [];
  // Function to iterate through the array
  let iterate = (arr, temp) => {
    // If the length of the temp array is greater than 4, return
    if (temp.length > 4) return;
    // If the length of the temp array is equal to 4 and the length of the arr is equal to 0, push the temp array to the result
    if (arr.length == 0 && temp.length == 4) {
      res.push(temp.join("."));
      return;
    }
    // Iterate through the array
    for (let i = 1; i < 4; i++) {
      // If the length of the arr is less than i, break
      if (arr.length < i) break;
      // Get the value
      let value = arr.slice(0, i);
      // If the length of the value is greater than 1 and the first element is equal to 0 or the value is greater than 255, break
      if ((value.length > 1 && value[0] == "0") || +value > 255) break;
      iterate(arr.slice(i), [...temp, value]);
    }
  };
  // Call the function
  iterate(s, []);
  // Return the result
  return res;
};
```
