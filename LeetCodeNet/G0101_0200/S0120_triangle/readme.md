[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 120\. Triangle

Medium

Given a `triangle` array, return _the minimum path sum from top to bottom_.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

**Example 1:**

**Input:** triangle = \[\[2],[3,4],[6,5,7],[4,1,8,3]]

**Output:** 11

**Explanation:**

    The triangle looks like:
        2
       3 4
      6 5 7
     4 1 8 3
     The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above). 

**Example 2:**

**Input:** triangle = \[\[-10]]

**Output:** -10 

**Constraints:**

*   `1 <= triangle.length <= 200`
*   `triangle[0].length == 1`
*   `triangle[i].length == triangle[i - 1].length + 1`
*   <code>-10<sup>4</sup> <= triangle[i][j] <= 10<sup>4</sup></code>

**Follow up:** Could you do this using only `O(n)` extra space, where `n` is the total number of rows in the triangle?

## Solution

```csharp
using System.Collections.Generic;

public class Solution {
    public int MinimumTotal(IList<IList<int>> triangle) {
        if (triangle == null || triangle.Count == 0) {
            return 0;
        }
        int n = triangle.Count;
        int[][] dp = new int[n][];
        for (int i = 0; i < n; i++) {
            dp[i] = new int[triangle[n - 1].Count];
            for (int j = 0; j < dp[i].Length; j++) {
                dp[i][j] = -10001;
            }
        }
        return Dfs(triangle, dp, 0, 0);
    }

    private int Dfs(IList<IList<int>> triangle, int[][] dp, int row, int col) {
        if (row >= triangle.Count) {
            return 0;
        }
        if (dp[row][col] != -10001) {
            return dp[row][col];
        }
        int sum = triangle[row][col] +
            System.Math.Min(Dfs(triangle, dp, row + 1, col), Dfs(triangle, dp, row + 1, col + 1));
        dp[row][col] = sum;
        return sum;
    }
}
```