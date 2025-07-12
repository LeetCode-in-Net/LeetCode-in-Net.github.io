[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 130\. Surrounded Regions

Medium

Given an `m x n` matrix `board` containing `'X'` and `'O'`, _capture all regions that are 4-directionally surrounded by_ `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

**Input:** board = \[\["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]

**Output:** [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]

**Explanation:** Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically. 

**Example 2:**

**Input:** board = \[\["X"]]

**Output:** [["X"]] 

**Constraints:**

*   `m == board.length`
*   `n == board[i].length`
*   `1 <= m, n <= 200`
*   `board[i][j]` is `'X'` or `'O'`.

## Solution

```csharp
public class Solution {
    public void Solve(char[][] board) {
        if (board.Length == 0) {
            return;
        }
        for (int i = 0; i < board[0].Length; i++) {
            if (board[0][i] == 'O') {
                Dfs(board, 0, i);
            }
            if (board[board.Length - 1][i] == 'O') {
                Dfs(board, board.Length - 1, i);
            }
        }
        for (int i = 0; i < board.Length; i++) {
            if (board[i][0] == 'O') {
                Dfs(board, i, 0);
            }
            if (board[i][board[0].Length - 1] == 'O') {
                Dfs(board, i, board[0].Length - 1);
            }
        }
        for (int i = 0; i < board.Length; i++) {
            for (int j = 0; j < board[0].Length; j++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
                if (board[i][j] == '#') {
                    board[i][j] = 'O';
                }
            }
        }
    }

    private void Dfs(char[][] board, int row, int column) {
        if (row < 0 || row >= board.Length || column < 0 || column >= board[0].Length || board[row][column] != 'O') {
            return;
        }
        board[row][column] = '#';
        Dfs(board, row + 1, column);
        Dfs(board, row - 1, column);
        Dfs(board, row, column + 1);
        Dfs(board, row, column - 1);
    }
}
```