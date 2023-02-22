---
layout: post
title: 787. Cheapest Flights Within K Stops
date: 2023-01-26 08:10 -0500
difficulty: medium
comments: true
---
There are `n` cities connected by some number of flights. You are given an array `flights` where `flights[i] = [fromi, toi, pricei]` indicates that there is a flight from city `fromi` to city `toi` with cost `pricei`.

You are also given three integers `src`, `dst`, and `k`, return **the cheapest price** from `src` to `dst` _with at most_ `k` stops. If there is no such route, return `-1`.\

<pre><strong>Input:</strong> n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
<strong>Output:</strong> 700
<strong>Explanation:</strong>
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.
Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.
</pre>

## Solution

```javascript
/**
 * @param {number} n
 * @param {number[][]} flights
 * @param {number} src
 * @param {number} dst
 * @param {number} k
 * @return {number}
 */
var findCheapestPrice = function(n, flights, src, dst, K) {
    //Declare a map to store the adjacency list
    const adjacencyList = new Map();
    //Iterate through the flights array and add the flights to the adjacency list
    for(let [start, end, cost] of flights) {
        //If the start city is already in the adjacency list, push the end city and cost to the array
        if(adjacencyList.has(start)) adjacencyList.get(start).push([end, cost]);
        //Else, create a new array with the end city and cost
        else adjacencyList.set(start, [[end, cost]]);
    }
    //Declare a queue to store the cities to visit
    const queue = [[0, src, K+1]];
    //Declare a map to store the visited cities
    const visited = new Map();
    //Iterate through the queue
    while(queue.length) {
        //Sort the queue by cost
        queue.sort((a, b) => a[0] - b[0]);
        //Pop the first element from the queue
        const [cost, city, stops] = queue.shift();
        //If the city has already been visited and the stops are greater than the current stops, continue
        visited.set(city, stops);
        //If the city is the destination, return the cost
        if(city === dst) return cost;
        //If the stops are less than or equal to 0 or the city is not in the adjacency list, continue
        if(stops <= 0 || !adjacencyList.has(city))  continue;
        //Iterate through the adjacency list
        for(let [nextCity, nextCost] of adjacencyList.get(city)) {
            //If the next city has already been visited and the stops are greater than or equal to the current stops, continue
            if(visited.has(nextCity) && visited.get(nextCity) >= stops-1) continue;
            //Push the next city to the queue
            queue.push([cost+nextCost, nextCity, stops-1]);
        }
    }
    //Return -1 if there is no path
    return -1;
};
```