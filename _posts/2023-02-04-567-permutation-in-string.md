---
layout: post
title: 567. Permutation in String
date: 2023-02-04 09:23 -0500
difficulty: medium
comments: true
---
Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` `if` one of `s1`'s permutations is the substring of `s2`.

## Example:
<pre><strong>Input:</strong> s1 = "ab", s2 = "eidbaooo"
<strong>Output:</strong> true
<strong>Explanation:</strong> s2 contains one permutation of s1 ("ba").
</pre>

```javascript
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var checkInclusion = function(s1, s2) {
    //declare a map
    let map = {}
    //declare a map2
    let map2 = {}

    let track = (fm,sm) =>{
        //loop through the map
        for(let i in fm){
            //if the map does not have the key return false
            if(!sm[i]) return false;
            //if the map value is not equal to the map2 value return false
            if(sm[i] != fm[i]) return false;
        }
        //return true
        return true;
    }
    for(let i =0; i<s1.length;i++){
        //if the map does not have the key create it
        map[s1[i]] = (map[s1[i]] || 0) + 1;
        //if the map2 does not have the key create it
        map2[s2[i]] = (map2[s2[i]] || 0) + 1;
    }
    for(let i =0; i<=s2.length - s1.length; i++){
        //if the map and map2 are equal return true
        if(track(map,map2)) return true;
        //if the map2 does not have the key create it
        map2[s2[i+s1.length]] = (map2[s2[i+s1.length]] || 0) + 1;
        //decrement the map2 value
        map2[s2[i]]--
    }
    //return the track function
    return track(map,map2);
};
```