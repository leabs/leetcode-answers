---
layout: post
title: 904. Fruit Into Baskets
date: 2023-02-07 08:57 -0500
difficulty: medium
comments: true
---

You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array `fruits` where `fruits[i]` is the type of fruit the `ith` tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

- You only have two baskets, and each basket can only hold a **single type** of fruit. There is no limit on the amount of fruit each basket can hold.
- Starting from any tree of your choice, you must pick **exactly one fruit** from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
- Once you reach a tree with fruit that cannot fit in your baskets, you must stop.

Given the integer array `fruits`, return the _maximum_ number of fruits you can pick.

## Example

<pre><strong>Input:</strong> fruits = [<u>1,2,1</u>]
<strong>Output:</strong> 3
<strong>Explanation:</strong> We can pick from all 3 trees.
</pre>

## Solution

```javascript
/**
 * @param {number[]} fruits
 * @return {number}
 */
const totalFruit = array => {
    //Create a map to store the current fruit and the count
    let map = new Map(), max = -1
    //Loop through the array
    for(let start = 0, end = 0; end < array.length; end++){
        //Get the current element
        let currElement = array[end]
        //Set the current element in the map
        map.set(currElement, map.get(currElement)+1 || 1 )
        //Check if the map size is greater than 2
        while(map.size > 2){
            //Get the current element
            let char = array[start]
            //Get the current element count
            let charCount = map.get(char)
            //Check if the count is 1
            if(charCount-1 === 0)map.delete(char)
            //Decrement the count
            else map.set(char, charCount-1)
            //Increment the start
            start++
        }
        //Check if the map size is greater than 1
        if(map.size >= 1)max = Math.max(max, end + 1 - start)
    }
    //Return max
    return max
};
```
