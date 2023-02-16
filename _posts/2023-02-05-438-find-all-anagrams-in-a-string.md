---
layout: post
title: 438. Find All Anagrams in a String
date: 2023-02-05 08:21 -0500
difficulty: medium
comments: true
---
Given two strings `s` and `p`, return an array of all the start indices of `p`'s anagrams in `s`. You may return the answer in any order.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Great solution with video [here!](https://leetcode.com/problems/find-all-anagrams-in-a-string/solutions/3143305/javascript-very-very-easy-to-understand-map-solution-with-video-explanation-en-kr/?orderBy=hot&languageTags=javascript)

## Example

<pre><strong>Input:</strong> s = "cbaebabacd", p = "abc"
<strong>Output:</strong> [0,6]
<strong>Explanation:</strong>
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
</pre>

```javascript
/**
 * @param {string} s
 * @param {string} p
 * @return {number[]}
 */
var findAnagrams = function(s, p) {
    //Declare a map
    let map = {}
    //Declare a map2
    let map2 = {}
    //Declare a result array
    let res = []
    //Declare a track function
    let track = (fm,sm) =>{
        for(let i in fm){
            //Check sm having same key as fm
            if(!sm[i]) return false;
            //Check sm having same values as fm
            if(sm[i] != fm[i]) return false;
        }
        return true;
    }
    
    for(let i =0; i<p.length;i++){
        //Declare a map with key as p[i] and value as 1
        map[p[i]] = (map[p[i]] || 0) + 1;
        //Declare a map2 with key as s[i] and value as 1
        map2[s[i]] = (map2[s[i]] || 0) + 1;
    }
    // s = "cbaebabacd" p ="abc"
    // map1 => a,b,c 
    // map2 => {c,b,a} -> {b,a,e} -> {a,e,b} -> {e,b,a} -> {b,a,b} -> {a,b,a} -> {b,a,c} -> {a,c,d}
    // result     O                                                                 O
    for(let i =0; i<=s.length - p.length; i++){
        //Check if map1 and map2 are same
        if(track(map,map2)) res.push(i);
        //Remove the first element from map2
        map2[s[i+p.length]] = (map2[s[i+p.length]] || 0) + 1;
        //Remove the first element from map2
        map2[s[i]]--
    }
    //Return the result
    return res;
};
```