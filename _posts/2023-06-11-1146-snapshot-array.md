---
layout: post
title: 1146. Snapshot Array
date: 2023-06-11 08:09 -0400
difficulty: medium
comments: true
---

Implement a SnapshotArray that supports the following interface:

- `SnapshotArray(int length)` initializes an array-like data structure with the given length. Initially, each element equals 0.
- `void set(index, val)` sets the element at the given `index` to be equal to val.
- `int snap()` takes a snapshot of the array and returns the `snap_id`: the total number of times we called snap() minus 1.
- `int get(index, snap_id)` returns the value at the given `index`, at the time we took the snapshot with the given `snap_id`

## Example

```javascript
Input: ["SnapshotArray","set","snap","set","get"]
[[3],[0,5],[],[0,6],[0,0]]
Output: [null,null,0,null,5]
Explanation:
SnapshotArray snapshotArr = new SnapshotArray(3); // set the length to be 3
snapshotArr.set(0,5);  // Set array[0] = 5
snapshotArr.snap();  // Take a snapshot, return snap_id = 0
snapshotArr.set(0,6);
snapshotArr.get(0,0);  // Get the value of array[0] with snap_id = 0, return 5
```

## Solution

Great solution found [here](https://leetcode.com/problems/snapshot-array/solutions/1763803/javascript/)

```javascript
/**
 * @param {number} length
 */
var SnapshotArray = function (length) {
  this.snaps = [...Array(length)].map(() => new Map());
  this.snapId = 0;
};

/**
 * @param {number} index
 * @param {number} val
 * @return {void}
 */
SnapshotArray.prototype.set = function (index, val) {
  this.snaps[index].set(this.snapId, val);
};

/**
 * @return {number}
 */
SnapshotArray.prototype.snap = function () {
  return this.snapId++;
};

/**
 * @param {number} index
 * @param {number} snap_id
 * @return {number}
 */
SnapshotArray.prototype.get = function (index, snap_id) {
  while (snap_id >= 0) {
    if (this.snaps[index].has(snap_id)) {
      return this.snaps[index].get(snap_id);
    }
    snap_id--;
  }
  return 0;
};

/**
 * Your SnapshotArray object will be instantiated and called as such:
 * var obj = new SnapshotArray(length)
 * obj.set(index,val)
 * var param_2 = obj.snap()
 * var param_3 = obj.get(index,snap_id)
 */
```
