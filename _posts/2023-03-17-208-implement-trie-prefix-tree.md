---
layout: post
title: 208. Implement Trie (Prefix Tree)
date: 2023-03-17 10:16 -0400
difficulty: medium
comments: true
---

A trie (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string `word` into the trie.
- `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

## Example

```javascript
Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
```

## Solution

Helpful solution found [here](https://leetcode.com/problems/implement-trie-prefix-tree/solutions/2619724/simple-clean-solution-js/?orderBy=hot&languageTags=javascript).

```javascript
//Class to represent a node in the trie
class TrieNode {
    constructor() {
    this.children = {}
    this.endWord = false
    }
}

var Trie = function() {
    //Initializes the trie object
    this.root = new TrieNode()
};

Trie.prototype.insert = function(word) {
    //Inserts the string word into the trie
    let curr = this.root
    for(let cha of word) {
        //if the character is not in the trie, add it
        if(!curr.children[cha]) {
            //create a new node for the character
             curr.children[cha] = new TrieNode()
        } 
        curr = curr.children[cha]
    }
    //mark the end of the word
    curr.endWord = true
};

//Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
Trie.prototype.search = function(word) {
    let curr = this.root
    for(let cha of word) {
        if(!curr.children[cha]) {
            return false
        }
        curr = curr.children[cha]
    }
    //if the word is a prefix of another word, return false
    return (curr.endWord == true) ? true : false
};

//Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.
Trie.prototype.startsWith = function(prefix) {
    let curr = this.root
    for(let cha of prefix) {
        if(!curr.children[cha]) {
            return false
        }
        //if the character is in the trie, move to the next character
        curr = curr.children[cha]
    }
    return true
};
```
