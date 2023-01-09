---
layout: post
title: "149. Max Points on a Line"
date: 2023-01-08 10:35:33 -0500
---
Given an array of `points` where `points[i] = [xi, yi]` represents a point on the X-Y plane, return *the maximum number of points that lie on the same straight line*.

```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var maxPoints = function(points) {
    //Set max to 0
    let max = 0;
    //find current slope from points array
    for (let i = 0; i < points.length; i++) {
        //Set current slope to 0
        let currentSlope = 0;
        //Set same to 1
        let same = 1;
        //Set slopeMap to a new map
        let slopeMap = new Map();
        //For loop to iterate through the points array
        for (let j = 0; j < points.length; j++) {
            //If i is not equal to j
            if (i !== j) {
                //Set x1 to points array at i at 0
                let x1 = points[i][0];
                //Set y1 to points array at i at 1
                let y1 = points[i][1];
                //Set x2 to points array at j at 0
                let x2 = points[j][0];
                //Set y2 to points array at j at 1
                let y2 = points[j][1];
                //Set slope to y2 minus y1 divided by x2 minus x1
                let slope = (y2 - y1) / (x2 - x1);
                //If x1 is equal to x2 and y1 is equal to y2
                if (x1 === x2 && y1 === y2) {
                    //Increment same
                    same++;
                } else {
                    //If slopeMap does not have the slope
                    if (!slopeMap.has(slope)) {
                        //Set slopeMap to slope and 1
                        slopeMap.set(slope, 1);
                    } else {
                        //Set slopeMap to slope and slopeMap at slope plus 1
                        slopeMap.set(slope, slopeMap.get(slope) + 1);
                    }
                    //Set current slope to Math.max of slopeMap at slope and current slope
                    currentSlope = Math.max(slopeMap.get(slope), currentSlope);
                }
            }
        }
        //Set max to Math.max of current slope plus same and max
        max = Math.max(currentSlope + same, max);
    }
    return max;
};
```