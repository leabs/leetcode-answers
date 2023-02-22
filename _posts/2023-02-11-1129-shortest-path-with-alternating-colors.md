---
layout: post
title: 1129. Shortest Path with Alternating Colors
date: 2023-02-11 08:01 -0500
difficulty: medium
comments: true
---
You are given an integer `n`, the number of nodes in a directed graph where the nodes are labeled from `0` to `n - 1`. Each edge is red or blue in this graph, and there could be self-edges and parallel edges.

You are given two arrays `redEdges` and `blueEdges` where:

- `redEdges[i] = [ai, bi]` indicates that there is a directed red edge from node `ai` to node `bi` in the graph, and
- `blueEdges[j] = [uj, vj]` indicates that there is a directed blue edge from node `uj` to node `vj` in the graph.

Return an array `answer` of length `n`, where each `answer[x]` is the length of the shortest path from node `0` to node `x` such that the edge colors alternate along the path, or `-1` if such a path does not exist.

## Example

```javascript
Input: n = 3, redEdges = [[0,1],[1,2]], blueEdges = []
Output: [0,1,-1]
```

Helpful solution found [here!](https://leetcode.com/problems/shortest-path-with-alternating-colors/solutions/3170113/96-55-fast-javascript-very-very-easy-to-understand-solution-with-video-explanation-en-kr/?orderBy=hot&languageTags=javascript)

## Solution

```javascript
/**
 * @param {number} n
 * @param {number[][]} redEdges
 * @param {number[][]} blueEdges
 * @return {number[]}
 */
var shortestAlternatingPaths = function(n, redEdges, blueEdges) {
    //makeMap takes in an array of edges and returns a map of the edges
    let makeMap = (edges) =>{
        let map = {}
        for(let [x,y] of edges){
            if(!map[x]) map[x] = []
            map[x].push(y)
        }
        return map
    }
    // 'red' => {...}
    // 'blue' => {...}
    let colorMap = {}
    colorMap['red'] = makeMap(redEdges)
    colorMap['blue'] = makeMap(blueEdges)
    
    let res = new Array(n).fill(-1)
    let q = []
    let visited = new Set();
    let count = 0;
    q.push(['red',0])
    q.push(['blue',0])
    visited.add('blue-0')
    visited.add('red-0')

    while(q.length > 0){
        let newQ = []

        //loop through all the nodes in the current level
        for(let [color,index] of q){
            //if we haven't visited this node yet, set the distance to the current count
            res[index] = res[index] == -1 ? count : Math.min(count,res[index])
            //if there are no more edges for this color, continue
            if(!colorMap[color][index]) continue;
            for(let path of colorMap[color][index]){
                //if we've already visited this node, continue
                let key = `${color}-${path}`;
                if(visited.has(key)) continue;
                visited.add(key)
                //add the new node to the queue
                let newColor = color == 'red' ? 'blue' : 'red'
                //add the new node to the queue
                newQ.push([newColor,path])
            }
        }
        //increment the count and set the new queue
        q = newQ;
        //increment the count
        count++
    }
    //return the result
    return res;
};
```