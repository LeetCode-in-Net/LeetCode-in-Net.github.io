[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 77\. Combinations

Medium

Given two integers `n` and `k`, return _all possible combinations of_ `k` _numbers out of the range_ `[1, n]`.

You may return the answer in **any order**.

**Example 1:**

**Input:** n = 4, k = 2

**Output:** [ [2,4], [3,4], [2,3], [1,2], [1,3], [1,4], ] 

**Example 2:**

**Input:** n = 1, k = 1

**Output:** [[1]] 

**Constraints:**

*   `1 <= n <= 20`
*   `1 <= k <= n`

## Solution

```csharp
public class Solution {
    public IList<IList<int>> Combine(int n, int k) {
        var res = new List<IList<int>>();
        Backtrack(1, n, k, new List<int>(), res);
        return res;
    }
    private void Backtrack(int start, int n, int k, List<int> curr, List<IList<int>> res) {
        if (curr.Count == k) {
            res.Add(new List<int>(curr));
            return;
        }
        for (int i = start; i <= n; i++) {
            curr.Add(i);
            Backtrack(i + 1, n, k, curr, res);
            curr.RemoveAt(curr.Count - 1);
        }
    }
}
```