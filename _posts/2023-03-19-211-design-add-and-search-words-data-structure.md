---
layout: post
title: 211. Design Add and Search Words Data Structure
date: 2023-03-19 10:06 -0400
difficulty: medium
comments: true
---

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

- `WordDictionary()` Initializes the object.
- `void addWord(word)` Adds `word` to the data structure, it can be matched later.
- `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

## Example

```javascript
Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]

Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```

## Solution

```javascript
var WordDictionary = function () {
  //Declare a root node
  this.n = {};
  this.isWord = false;
  return this;
};

/**
 * @param {string} word
 * @return {void}
 */
WordDictionary.prototype.addWord = function (word) {
  //Declare a current node
  let curr = this;
  //Loop through the word
  for (let i = 0; i < word.length; i++) {
    if (!curr.n[word[i]]) {
      //If the current node does not have the letter, add it
      curr.n[word[i]] = new WordDictionary(word[i]);
    }
    curr = curr.n[word[i]];
  }
  //Set the last node to be a word
  curr.isWord = true;
};

/**
 * @param {string} word
 * @return {boolean}
 */
WordDictionary.prototype.search = function (word, start = 0, newCurr = null) {
  let curr = this;
  //If a new current node is passed in, set it to be the current node
  if (newCurr != null) curr = newCurr;
  for (let i = start; i < word.length; i++) {
    let char = word[i];
    if (char == ".") {
      let letters = Object.keys(curr.n);
      let res = false;
      for (let letter of letters) {
        //Recursively call search on each letter
        res = res || this.search(word, i + 1, curr.n[letter]);
      }
      return res;
    } else if (!curr.n[char]) {
      return false;
    }
    //Set the current node to be the next letter
    curr = curr.n[char];
  }
  return curr.isWord;
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * var obj = new WordDictionary()
 * obj.addWord(word)
 * var param_2 = obj.search(word)
 */
```
