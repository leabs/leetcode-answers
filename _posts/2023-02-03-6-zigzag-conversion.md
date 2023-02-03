---
layout: post
title: 6. Zigzag Conversion
date: 2023-02-03 10:21 -0500
difficulty: medium
comments: true
---
The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

<pre>P   A   H   N
A P L S I I G
Y   I   R
</pre>
And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

<pre>
string convert(string s, int numRows);
</pre>

## Example:
<pre><strong>Input:</strong> s = "PAYPALISHIRING", numRows = 3
<strong>Output:</strong> "PAHNAPLSIIGYIR"
</pre>

```javascript
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    //Declare a result array
    let res = [];
    //Declare a count variable
    let count = 0;
    //Declare a up variable
    let up = true;
    //Loop through the string
    for(let i =0; i<s.length;i++){
        //if the result array does not have the count index create it
        if(!res[count]) res[count] = []
        res[count].push(s[i])
        //increment or decrement the count
        count = up ? count+1 : count-1
        //if the count is equal to the number of rows or 0 change the direction
        if(count+1 == numRows) up = false;
        //if the count is equal to 0 change the direction
        else if(count == 0) up = true;
    }
    //declare a result variable
    let result = ''
    //loop through the result array and join the array
    for(let i of res){
        result += i.join('')
    }
    //return the result
    return result;
};
```