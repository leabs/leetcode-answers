---
layout: post
title: 909. Snakes and Ladders
date: 2023-01-24 21:00 -0500
difficulty: medium
comments: true
---

You are given an `n x n` integer matrix `board` where the cells are labeled from `1` to `n2` in a Boustrophedon style starting from the bottom left of the board (i.e. `board[n - 1][0]`) and alternating direction each row.

You start on square `1` of the board. In each move, starting from square `curr`, do the following:

- Choose a destination square `next` with a label in the range `[curr + 1, min(curr + 6, n2)]`.
  - This choice simulates the result of a standard 6-sided die roll: i.e., there are always at most 6 destinations, regardless of the size of the board.

- If `next` has a snake or ladder, you must move to the destination of that snake or ladder. Otherwise, you move to `next`.

- The game ends when you reach the square n2.

A board square on row `r` and column `c` has a snake or ladder if `board[r][c] != -1`. The destination of that snake or ladder is `board[r][c]`. Squares `1` and `n2` do not have a snake or ladder.

Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do not follow the subsequent snake or ladder.

For example, suppose the board is `[[-1,4],[-1,3]]`, and on the first move, your destination square is `2`. You follow the ladder to square `3`, but do not follow the subsequent ladder to `4`.

Return _the least number of moves required to reach the square_ `n2`. If it is not possible to reach the square, return `-1`.

## Example

```javascript
Input: board = [[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,35,-1,-1,13,-1],[-1,-1,-1,-1,-1,-1],[-1,15,-1,-1,-1,-1]]
Output: 4
Explanation: 
In the beginning, you start at square 1 (at row 5, column 0).
You decide to move to square 2 and must take the ladder to square 15.
You then decide to move to square 17 and must take the snake to square 13.
You then decide to move to square 14 and must take the ladder to square 35.
You then decide to move to square 36, ending the game.
This is the lowest possible number of moves to reach the last square, so return 4.
```

## Solution

```javascript
/**
 * @param {number[][]} board
 * @return {number}
 */
var snakesAndLadders = function (board) {
  //set n to be the length of the board
  let n = board.length;
  //create a set to store the visited positions
  let set = new Set();
  //create a function to get the position of the board
  let getPos = (pos) => {
    //get the row and column of the position
    let row = Math.floor((pos - 1) / n);
    let col = (pos - 1) % n;
    col = row % 2 == 1 ? n - 1 - col : col;
    row = n - 1 - row;
    //return
    return [row, col];
  };
  //create a queue to store the positions and moves
  let q = [[1, 0]];
  //loop through the queue
  while (q.length > 0) {
    //get the position and moves
    [pos, moves] = q.shift();
    //loop through the next 6 positions
    for (let i = 1; i < 7; i++) {
      let newPos = i + pos;
      let [r, c] = getPos(newPos);
      //if the position is a snake or ladder, get the new position
      if (board[r][c] != -1) newPos = board[r][c];
      //if the position is the last position, return the moves
      if (newPos == n * n) return moves + 1;
      //if the position is not visited, add it to the set and push it to the queue
      if (!set.has(newPos)) {
        set.add(newPos);
        q.push([newPos, moves + 1]);
      }
    }
  }
  //if the queue is empty, return -1
  return -1;
};
```
