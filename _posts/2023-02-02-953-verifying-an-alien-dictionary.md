---
layout: post
title: 953. Verifying an Alien Dictionary
date: 2023-02-02 09:16 -0500
difficulty: easy
comments: true
---
In an alien language, surprisingly, they also use English lowercase letters, but possibly in a different `order`. The `order` of the alphabet is some permutation of lowercase letters.

Given a sequence of `words` written in the alien language, and the `order` of the alphabet, return `true` if and only if the given `words` are sorted lexicographically in this alien language.

## Example

<pre><strong>Input:</strong> words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
<strong>Output:</strong> true
<strong>Explanation: </strong>As 'h' comes before 'l' in this language, then the sequence is sorted.
</pre>

## Solution

```javascript
/**
 * @param {string[]} words
 * @param {string} order
 * @return {boolean}
 */
var isAlienSorted = function(words, order) {
    // create a map for order
    let orderMap = {}
    // loop through order and create a map
    for(let o =0; o < order.length; o++){
        // map the order to the index
        orderMap[order[o]] = o;
    }
    // create a function to validate the order
    let isValidate = (c,p) =>{
        // get the length of the shortest word
        let len = c.length < p.length ? c.length : p.length;
        
        for(let i =0; i<len; i++){
            // if the current word is greater than the previous word return true
            if(orderMap[c[i]] > orderMap[p[i]]) return true;
            // if the current word is less than the previous word return false
            if(orderMap[c[i]] < orderMap[p[i]]) return false;
        }
        // if the current word is greater than the previous word return true
        return c.length >= p.length;
    }
    for(let i =1; i<words.length;i++){
        // if the word is not valid return false
        if(!isValidate(words[i],words[i-1])) return false;
    }
    // return true
    return true; 
};
```