[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 52\. N-Queens II

Hard

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _the number of distinct solutions to the **n-queens puzzle**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4

**Output:** 2

**Explanation:** There are two distinct solutions to the 4-queens puzzle as shown. 

**Example 2:**

**Input:** n = 1

**Output:** 1 

**Constraints:**

*   `1 <= n <= 9`

## Solution

```csharp
public class Solution {
    public int TotalNQueens(int n) {
        int count = 0;
        Solve(0, n, new bool[n], new bool[2 * n], new bool[2 * n], ref count);
        return count;
    }

    private void Solve(int row, int n, bool[] cols, bool[] d1, bool[] d2, ref int count) {
        if (row == n) {
            count++;
            return;
        }
        for (int col = 0; col < n; col++) {
            int id1 = col - row + n;
            int id2 = col + row;
            if (cols[col] || d1[id1] || d2[id2]) continue;
            cols[col] = d1[id1] = d2[id2] = true;
            Solve(row + 1, n, cols, d1, d2, ref count);
            cols[col] = d1[id1] = d2[id2] = false;
        }
    }
}
```