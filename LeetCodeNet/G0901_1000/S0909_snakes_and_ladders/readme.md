[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 909\. Snakes and Ladders

Medium

You are given an `n x n` integer matrix `board` where the cells are labeled from `1` to <code>n<sup>2</sup></code> in a [**Boustrophedon style**](https://en.wikipedia.org/wiki/Boustrophedon) starting from the bottom left of the board (i.e. `board[n - 1][0]`) and alternating direction each row.

You start on square `1` of the board. In each move, starting from square `curr`, do the following:

*   Choose a destination square `next` with a label in the range <code>[curr + 1, min(curr + 6, n<sup>2</sup>)]</code>.
    *   This choice simulates the result of a standard **6-sided die roll**: i.e., there are always at most 6 destinations, regardless of the size of the board.
*   If `next` has a snake or ladder, you **must** move to the destination of that snake or ladder. Otherwise, you move to `next`.
*   The game ends when you reach the square <code>n<sup>2</sup></code>.

A board square on row `r` and column `c` has a snake or ladder if `board[r][c] != -1`. The destination of that snake or ladder is `board[r][c]`. Squares `1` and <code>n<sup>2</sup></code> do not have a snake or ladder.

Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do **not** follow the subsequent snake or ladder.

*   For example, suppose the board is `[[-1,4],[-1,3]]`, and on the first move, your destination square is `2`. You follow the ladder to square `3`, but do **not** follow the subsequent ladder to `4`.

Return _the least number of moves required to reach the square_ <code>n<sup>2</sup></code>_. If it is not possible to reach the square, return_ `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/09/23/snakes.png)

**Input:** board = \[\[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,35,-1,-1,13,-1],[-1,-1,-1,-1,-1,-1],[-1,15,-1,-1,-1,-1]]

**Output:** 4

**Explanation:** 

In the beginning, you start at square 1 (at row 5, column 0). 

You decide to move to square 2 and must take the ladder to square 15. 

You then decide to move to square 17 and must take the snake to square 13. 

You then decide to move to square 14 and must take the ladder to square 35. 

You then decide to move to square 36, ending the game. 

This is the lowest possible number of moves to reach the last square, so return 4.

**Example 2:**

**Input:** board = \[\[-1,-1],[-1,3]]

**Output:** 1

**Constraints:**

*   `n == board.length == board[i].length`
*   `2 <= n <= 20`
*   `grid[i][j]` is either `-1` or in the range <code>[1, n<sup>2</sup>]</code>.
*   The squares labeled `1` and <code>n<sup>2</sup></code> do not have any ladders or snakes.

## Solution

```csharp
using System;
using System.Collections.Generic;

public class Solution {
    private int size;

    public int SnakesAndLadders(int[][] board) {
        Queue<int> queue = new Queue<int>();
        size = board.Length;
        int target = size * size;
        // Using 0-indexed for visited array, corresponding to labels 1 to target
        bool[] visited = new bool[target];
        queue.Enqueue(1);
        // Mark label 1 as visited (index 0)
        visited[0] = true;
        int step = 0;
        while (queue.Count > 0) {
            int queueSize = queue.Count;
            for (int i = 0; i < queueSize; i++) {
                int previousLabel = queue.Dequeue();
                if (previousLabel == target) {
                    return step;
                }
                // Simulate rolling a die (1 to 6)
                for (int currentLabel = previousLabel + 1;
                     currentLabel <= Math.Min(target, previousLabel + 6);
                     currentLabel++) {
                    // currentLabel - 1 to map to 0-indexed array
                    if (visited[currentLabel - 1]) {
                        continue;
                    }
                    // Mark as visited
                    visited[currentLabel - 1] = true;
                    int[] position = IndexToPosition(currentLabel);
                    int boardValue = board[position[0]][position[1]];

                    if (boardValue == -1) {
                        queue.Enqueue(currentLabel);
                    } else {
                        queue.Enqueue(boardValue);
                    }
                }
            }
            step++;
        }
        // Target not reachable
        return -1;
    }

    private int[] IndexToPosition(int index) {
        // Adjust index to be 0-based for calculations related to 0 to size*size - 1
        int adjustedIndex = index - 1;
        // Calculate row
        // From bottom to top, so (size - 1) - (row based on adjustedIndex)
        int row = size - 1 - adjustedIndex / size;
        // Calculate column
        int col;
        // Check if the row is "snake" (even from bottom) or "ladder" (odd from bottom)
        // (size - 1 - row) gives the 0-indexed row number from the top of the board.
        // If (size - 1 - row) is even, it's a left-to-right row.
        // If (size - 1 - row) is odd, it's a right-to-left row.
        // The original Java code uses (this.size - vertical) % 2 == 1,
        // which corresponds to (row from top of board) % 2 == 1,
        // meaning if the row is odd (0-indexed from top), it's left-to-right
        // If row from top is 0 (bottom row), 2, 4... then it's left to right.
        // If row from top is 1, 3, 5... then it's right to left.
        // (size - 1 - row) is equivalent to the number of rows from the bottom.
        // (size - 1 - vertical) is a more direct translation from the Java code.
        if ((size - 1 - row) % 2 == 0) { // Even row from top (0-indexed), moves right (left to right)
            col = adjustedIndex % size;
        } else {
            // Odd row from top (0-indexed), moves left (right to left)
            col = size - 1 - (adjustedIndex % size);
        }
        return new int[] {row, col};
    }
}
```