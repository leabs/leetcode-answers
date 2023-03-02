---
layout: post
title: 443. String Compression
date: 2023-03-02 08:17 -0500
difficulty: medium
comments: true
---

Given an array of characters `chars`, compress it using the following algorithm:

Begin with an empty string `s`. For each group of consecutive repeating characters in `chars`:

- If the group's length is `1`, append the character to `s`.
- Otherwise, append the character followed by the group's length.

The compressed string `s` **should not be returned separately**, but instead, be stored in the input character array `chars`. Note that group lengths that are 10 or longer will be split into multiple characters in `chars`.

After you are done **modifying the input array**, return the new length of the array.

You must write an algorithm that uses only constant extra space.

## Example

```javascript
Input: chars = ["a","a","b","b","c","c","c"]
Output: Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]
Explanation: The groups are "aa", "bb", and "ccc". This compresses to "a2b2c3".
```

## Solution

```javascript
/**
 * @param {character[]} chars
 * @return {number}
 */
var compress = function (chars) {
  // Begin with an empty string `s`. For each group of consecutive repeating characters in `chars`:
  let s = "";

  // If the group's length is `1`, append the character to `s`.
  if (chars.length === 1) {
    s += chars[0];
  }
  //If the group's length is greater than 1, return the amount of instances with a number
  else {
    //Set the current character to the first character in the array
    let currentChar = chars[0];
    //Set the current count to 1
    let currentCount = 1;
    //Loop through the array
    for (let i = 1; i < chars.length; i++) {
      //If the current character is equal to the next character, increment the count
      if (currentChar === chars[i]) {
        currentCount++;
      }
      //If the current character is not equal to the next character, add the current character and the count to the string
      else {
        s += currentChar;
        //If the count is greater than 1, add the count to the string
        if (currentCount > 1) {
          s += currentCount;
        }
        //Set the current character to the next character
        currentChar = chars[i];
        //Set the current count to 1
        currentCount = 1;
      }
    }
    //Add the last character and count to the string
    s += currentChar;
    if (currentCount > 1) {
      s += currentCount;
    }
  }
  //Set the length of the array to the length of the string
  chars.length = s.length;
  //Loop through the string and set the characters in the array to the characters in the string
  for (let i = 0; i < s.length; i++) {
    chars[i] = s[i];
  }
  //Return the length of the array
  return chars.length;
};
```
