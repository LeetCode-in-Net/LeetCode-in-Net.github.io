[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 149\. Max Points on a Line

Hard

Given an array of `points` where <code>points[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> represents a point on the **X-Y** plane, return _the maximum number of points that lie on the same straight line_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/25/plane1.jpg)

**Input:** points = \[\[1,1],[2,2],[3,3]]

**Output:** 3 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/25/plane2.jpg)

**Input:** points = \[\[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]

**Output:** 4 

**Constraints:**

*   `1 <= points.length <= 300`
*   `points[i].length == 2`
*   <code>-10<sup>4</sup> <= x<sub>i</sub>, y<sub>i</sub> <= 10<sup>4</sup></code>
*   All the `points` are **unique**.

## Solution

```csharp
public class Solution {
    public int MaxPoints(int[][] points) {
        if (points.Length < 2) {
            return points.Length;
        }
        int max = 0;
        for (int i = 0; i < points.Length; i++) {
            for (int j = i + 1; j < points.Length; j++) {
                int x = points[j][0] - points[i][0];
                int y = points[j][1] - points[i][1];
                int c = x * points[j][1] - y * points[j][0];
                int count = 2;
                for (int k = j + 1; k < points.Length; k++) {
                    if (c == x * points[k][1] - y * points[k][0]) {
                        count++;
                    }
                }
                max = System.Math.Max(count, max);
            }
        }
        return max;
    }
}
```