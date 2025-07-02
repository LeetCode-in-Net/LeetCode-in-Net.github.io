[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 36\. Valid Sudoku

Medium

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1.  Each row must contain the digits `1-9` without repetition.
2.  Each column must contain the digits `1-9` without repetition.
3.  Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

*   A Sudoku board (partially filled) could be valid but is not necessarily solvable.
*   Only the filled cells need to be validated according to the mentioned rules.

**Example 1:**

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

**Input:** board = 

[["5","3",".",".","7",".",".",".","."] ,

["6",".",".","1","9","5",".",".","."] ,

[".","9","8",".",".",".",".","6","."] ,

["8",".",".",".","6",".",".",".","3"] ,

["4",".",".","8",".","3",".",".","1"] ,

["7",".",".",".","2",".",".",".","6"] ,

[".","6",".",".",".",".","2","8","."] ,

[".",".",".","4","1","9",".",".","5"] ,

[".",".",".",".","8",".",".","7","9"]]

**Output:** true

**Example 2:**

**Input:** board = 

[["8","3",".",".","7",".",".",".","."] ,

["6",".",".","1","9","5",".",".","."] ,

[".","9","8",".",".",".",".","6","."] ,

["8",".",".",".","6",".",".",".","3"] ,

["4",".",".","8",".","3",".",".","1"] ,

["7",".",".",".","2",".",".",".","6"] ,

[".","6",".",".",".",".","2","8","."] ,

[".",".",".","4","1","9",".",".","5"] ,

[".",".",".",".","8",".",".","7","9"]]

**Output:** false

**Explanation:** Same as Example 1, except with the **5** in the top left corner being modified to **8**. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

**Constraints:**

*   `board.length == 9`
*   `board[i].length == 9`
*   `board[i][j]` is a digit `1-9` or `'.'`.

## Solution

```csharp
using System.Collections.Generic;

public class Solution {
    public bool IsValidSudoku(char[][] board) {
        bool[,] rows = new bool[9, 9];
        bool[,] cols = new bool[9, 9];
        bool[,] blocks = new bool[9, 9];
        for (int i = 0; i < board.Length; i++) {
            for (int j = i; j < board[i].Length; j++) {
                if (!isValidCase(board, i, j, rows, cols, blocks)) {
                    return false;
                }
                if (i != j && !isValidCase(board, j, i, rows, cols, blocks)) {
                    return false;
                }
            }
        }
        return true;
    }

    private bool isValidCase(char[][] board, int i, int j, bool[,] rows, bool[,] cols, bool[,] blocks) {
        if (board[i][j] == '.')
            return true;
        int num = board[i][j] - '1';
        int block = (i / 3) * 3 + (j / 3);
        if (rows[i, num] || cols[j, num] || blocks[block, num])
            return false;
        rows[i, num] = true;
        cols[j, num] = true;
        blocks[block, num] = true;
        return true;
    }
}
```