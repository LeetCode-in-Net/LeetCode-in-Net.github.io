[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 63\. Unique Paths II

Medium

A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and space is marked as `1` and `0` respectively in the grid.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

**Input:** obstacleGrid = \[\[0,0,0],[0,1,0],[0,0,0]]

**Output:** 2

**Explanation:** There is one obstacle in the middle of the 3x3 grid above. There are two ways to reach the bottom-right corner: 1. Right -> Right -> Down -> Down 2. Down -> Down -> Right -> Right 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)

**Input:** obstacleGrid = \[\[0,1],[0,0]]

**Output:** 1 

**Constraints:**

*   `m == obstacleGrid.length`
*   `n == obstacleGrid[i].length`
*   `1 <= m, n <= 100`
*   `obstacleGrid[i][j]` is `0` or `1`.

## Solution

```csharp
public class Solution {
    public int UniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.Length;
        int  n = obstacleGrid[0].Length;
        int[,] dp = new int[m, n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (obstacleGrid[i][j] == 1) {
                    dp[i, j] = 0;
                } else if (i == 0 && j == 0) {
                    dp[i, j] = 1;
                } else {
                    dp[i, j] = (i > 0 ? dp[i - 1, j] : 0) + (j > 0 ? dp[i, j - 1] : 0);
                }
            }
        }
        return dp[m - 1, n - 1];
    }
}
```