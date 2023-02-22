---
layout: post
title: 352. Data Stream as Disjoint Intervals
date: 2023-01-28 08:14 -0500
difficulty: hard
comments: true
---
Given a data stream input of non-negative integers `a1, a2, ..., an`, summarize the numbers seen so far as a list of disjoint intervals.

Implement the `SummaryRanges` class:

- `SummaryRanges()` Initializes the object with an empty stream.

- `void addNum(int value)` Adds the integer `value` to the stream.

- `int[][] getIntervals()` Returns a summary of the integers in the stream currently as a list of disjoint intervals `[starti, endi]`. The answer should be sorted by `starti`.

Great solution with video [here.](https://leetcode.com/problems/data-stream-as-disjoint-intervals/solutions/3107479/100-javascript-fast-very-very-easy-to-understand-with-video-explanation/?orderBy=hot&languageTags=javascript)

<pre><strong>Input</strong>
["SummaryRanges", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals", "addNum", "getIntervals"]
[[], [1], [], [3], [], [7], [], [2], [], [6], []]
<strong>Output</strong>
[null, null, [[1, 1]], null, [[1, 1], [3, 3]], null, [[1, 1], [3, 3], [7, 7]], null, [[1, 3], [7, 7]], null, [[1, 3], [6, 7]]]

<strong>Explanation</strong>
SummaryRanges summaryRanges = new SummaryRanges();
summaryRanges.addNum(1);      // arr = [1]
summaryRanges.getIntervals(); // return [[1, 1]]
summaryRanges.addNum(3);      // arr = [1, 3]
summaryRanges.getIntervals(); // return [[1, 1], [3, 3]]
summaryRanges.addNum(7);      // arr = [1, 3, 7]
summaryRanges.getIntervals(); // return [[1, 1], [3, 3], [7, 7]]
summaryRanges.addNum(2);      // arr = [1, 2, 3, 7]
summaryRanges.getIntervals(); // return [[1, 3], [7, 7]]
summaryRanges.addNum(6);      // arr = [1, 2, 3, 6, 7]
summaryRanges.getIntervals(); // return [[1, 3], [6, 7]]
</pre>

## Solution

```javascript
var SummaryRanges = function() {
    this.arr = []
};

/** 
 * @param {number} value
 * @return {void}
 */
SummaryRanges.prototype.addNum = function(val) {
    // Declare a variable to check if the value is inside the array
    let valIsInside = false;
    for(let i =0; i<this.arr.length;i++){
        // Destructure the array
        let [x,y] = this.arr[i];
        // Check if the value is inside the array
        if(val >=x && val<=y){
            // If it is, set the variable to true and break out of the loop
            valIsInside = true;
            break;
        }
        else if(val === y + 1){
            // If the value is one more than the end of the interval, set the end of the interval to the value
            this.arr[i][1] = val;
            if(val + 1 === this.arr[i+1]?.[0]){
                // If the value is one more than the start of the next interval, set the end of the interval to the start of the next interval
                this.arr[i][1] = this.arr[i+1][1]
                // Remove the next interval
                this.arr.splice(i+1,1)
            }
            valIsInside = true;
            break;
        }
        else if(val < x){
            if(val + 1 == x){
                // If the value is one less than the start of the interval, set the start of the interval to the value
                this.arr[i][0] = val;
            }
            // If the value is less than the start of the interval, insert the value into the array
            else this.arr.splice(i,0,[val,val])
            valIsInside = true;
            break;
        }
    }
    // If the value is not inside the array, push it into the array
    if(!valIsInside) this.arr.push([val,val])
};

/**
 * @return {number[][]}
 */
SummaryRanges.prototype.getIntervals = function() {
    return this.arr
};
```
