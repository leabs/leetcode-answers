---
layout: post
title: 909. Snakes and Ladders
date: 2023-01-24 21:00 -0500
difficulty: medium
comments: true
---

<div class="_1l1MA"><p>You are given an <code>n x n</code> integer matrix <code>board</code> where the cells are labeled from <code>1</code> to <code>n<sup>2</sup></code> in a <a href="https://en.wikipedia.org/wiki/Boustrophedon" target="_blank"><strong>Boustrophedon style</strong></a> starting from the bottom left of the board (i.e. <code>board[n - 1][0]</code>) and alternating direction each row.</p>

<p>You start on square <code>1</code> of the board. In each move, starting from square <code>curr</code>, do the following:</p>

<ul>
	<li>Choose a destination square <code>next</code> with a label in the range <code>[curr + 1, min(curr + 6, n<sup>2</sup>)]</code>.

    <ul>
    	<li>This choice simulates the result of a standard <strong>6-sided die roll</strong>: i.e., there are always at most 6 destinations, regardless of the size of the board.</li>
    </ul>
    </li>
    <li>If <code>next</code> has a snake or ladder, you <strong>must</strong> move to the destination of that snake or ladder. Otherwise, you move to <code>next</code>.</li>
    <li>The game ends when you reach the square <code>n<sup>2</sup></code>.</li>

</ul>

<p>A board square on row <code>r</code> and column <code>c</code> has a snake or ladder if <code>board[r][c] != -1</code>. The destination of that snake or ladder is <code>board[r][c]</code>. Squares <code>1</code> and <code>n<sup>2</sup></code> do not have a snake or ladder.</p>

<p>Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do <strong>not</strong> follow the subsequent&nbsp;snake or ladder.</p>

<ul>
	<li>For example, suppose the board is <code>[[-1,4],[-1,3]]</code>, and on the first move, your destination square is <code>2</code>. You follow the ladder to square <code>3</code>, but do <strong>not</strong> follow the subsequent ladder to <code>4</code>.</li>
</ul>

<p>Return <em>the least number of moves required to reach the square </em><code>n<sup>2</sup></code><em>. If it is not possible to reach the square, return </em><code>-1</code>.</p></div>

<pre><strong>Input:</strong> board = [[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,35,-1,-1,13,-1],[-1,-1,-1,-1,-1,-1],[-1,15,-1,-1,-1,-1]]
<strong>Output:</strong> 4
<strong>Explanation:</strong> 
In the beginning, you start at square 1 (at row 5, column 0).
You decide to move to square 2 and must take the ladder to square 15.
You then decide to move to square 17 and must take the snake to square 13.
You then decide to move to square 14 and must take the ladder to square 35.
You then decide to move to square 36, ending the game.
This is the lowest possible number of moves to reach the last square, so return 4.
</pre>

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
