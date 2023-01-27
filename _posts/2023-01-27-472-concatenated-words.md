---
layout: post
title: 472. Concatenated Words
date: 2023-01-27 08:44 -0500
difficulty: hard
comments: true
---
Given an array of strings **words** `(without duplicates)`, return all the concatenated words in the given list of `words`.

A **concatenated word** is defined as a string that is comprised entirely of at least two shorter words in the given array.

<pre><strong>Input:</strong> words = ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
<strong>Output:</strong> ["catsdogcats","dogcatsdog","ratcatdogcat"]
<strong>Explanation:</strong> "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
"dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
"ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".</pre>


```javascript
/**
 * @param {string[]} words
 * @return {string[]}
 */
var findAllConcatenatedWordsInADict = function(words) {
    //Declare a set to store all the words
    const set = new Set(words);
    //Declare a result array
    let res = []
    //Declare a function to check if the word is valid
    let isValid = (word) =>{
        //If the word is empty, return true
        if(word.length == 0) return true;
        //Loop through the word
        for(let i =1; i<=word.length;i++){
            //Get the substring from 0 to i
            let value = word.slice(0,i);
            //If the substring is in the set, check if the rest of the word is valid
            if(set.has(value)){
                //If the rest of the word is valid, return true
                let check = isValid(word.slice(i))
                if(check) return true;
            }
        }
        //If the word is not valid, return false
        return false;
    }
    //Loop through the words
    for(let word of words){
        //Remove the word from the set
        set.delete(word);
        //Check if the word is valid if it is push it to the result array
        if(isValid(word)) res.push(word)
        //Add the word back to the set
        set.add(word)
    }
    //Return the result array
    return res;
};
```