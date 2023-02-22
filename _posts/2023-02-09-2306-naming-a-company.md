---
layout: post
title: 2306. Naming a Company
date: 2023-02-09 09:47 -0500
difficulty: hard
comments: true
---
You are given an array of strings `ideas` that represents a list of names to be used in the process of naming a company. The process of naming a company is as follows:

Choose 2 distinct names from `ideas`, call them `ideaA` and `ideaB`.
Swap the first letters of `ideaA` and `ideaB` with each other.
If **both** of the new names are not found in the original `ideas`, then the name `ideaA ideaB` (the **concatenation** of `ideaA` and `ideaB`, separated by a space) is a valid company name.
Otherwise, it is not a valid name.
Return the number of _distinct_ valid names for the company.

## Example:
<pre><strong>Input:</strong> ideas = ["coffee","donuts","time","toffee"]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The following selections are valid:
- ("coffee", "donuts"): The company name created is "doffee conuts".
- ("donuts", "coffee"): The company name created is "conuts doffee".
- ("donuts", "time"): The company name created is "tonuts dime".
- ("donuts", "toffee"): The company name created is "tonuts doffee".
- ("time", "donuts"): The company name created is "dime tonuts".
- ("toffee", "donuts"): The company name created is "doffee tonuts".
Therefore, there are a total of 6 distinct company names.

The following are some examples of invalid selections:
- ("coffee", "time"): The name "toffee" formed after swapping already exists in the original array.
- ("time", "toffee"): Both names are still the same after swapping and exist in the original array.
- ("coffee", "toffee"): Both names formed after swapping already exist in the original array.
</pre>

Great explaination to this problem [here](https://leetcode.com/problems/naming-a-company/solutions/3162412/100-fast-javascript-very-very-easy-to-understand-solution-with-video-explanation-en-kr/?orderBy=hot&languageTags=javascript).

## Solution

```javascript
/**
 * @param {string[]} ideas
 * @return {number}
 */
var distinctNames = function(ideas) {
    // we have to avoid using same start ch
    // we have to avoid using same other ch
    //["cake","coffee","donuts","time","toffee"]
    // cake    toffee
    // coffee  time

    // cake   donuts
    // coffee
    // 2 * (ch1.size - sameCount) * (ch2.size - sameCount)

    let map = {}

    //Loop through the array
    for(let idea of ideas){
        //Get the first character
        let firstC = idea.slice(0,1)
        //Get the rest of the characters
        let others = idea.slice(1)
        //Check if the first character is in the map
        if(!map[firstC]) map[firstC] = new Set()
        //Add the rest of the characters to the map
        map[firstC].add(others)
    }
    
    //Get the keys
    let keys = Object.keys(map);
    let count = 0;

    for(let i =0; i<keys.length; i++){
        //Get the first set
        let firstSet = map[keys[i]]
        //Loop through the rest of the keys
        for(let j =i+1; j<keys.length; j++){
            //Get the second set
            let secondSet = map[keys[j]]
            //Get the same count
            let sameCount = 0;
            //Loop through the first set
            for(let c of firstSet){
                //Check if the second set has the same character
                if(secondSet.has(c)) sameCount++ 
            }
            //Add to the count
            count += 2 * (firstSet.size - sameCount) * (secondSet.size - sameCount)
        }
    }
    //Return the count
    return count;
};

```