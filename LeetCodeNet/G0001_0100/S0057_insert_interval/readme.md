[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 57\. Insert Interval

Medium

You are given an array of non-overlapping intervals `intervals` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represent the start and the end of the <code>i<sup>th</sup></code> interval and `intervals` is sorted in ascending order by <code>start<sub>i</sub></code>. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by <code>start<sub>i</sub></code> and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` _after the insertion_.

**Example 1:**

**Input:** intervals = \[\[1,3],[6,9]], newInterval = [2,5]

**Output:** [[1,5],[6,9]] 

**Example 2:**

**Input:** intervals = \[\[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]

**Output:** [[1,2],[3,10],[12,16]]

**Explanation:** Because the new interval `[4,8]` overlaps with `[3,5],[6,7],[8,10]`.

**Example 3:**

**Input:** intervals = [], newInterval = [5,7]

**Output:** [[5,7]] 

**Example 4:**

**Input:** intervals = \[\[1,5]], newInterval = [2,3]

**Output:** [[1,5]] 

**Example 5:**

**Input:** intervals = \[\[1,5]], newInterval = [2,7]

**Output:** [[1,7]] 

**Constraints:**

*   <code>0 <= intervals.length <= 10<sup>4</sup></code>
*   `intervals[i].length == 2`
*   <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>5</sup></code>
*   `intervals` is sorted by <code>start<sub>i</sub></code> in **ascending** order.
*   `newInterval.length == 2`
*   <code>0 <= start <= end <= 10<sup>5</sup></code>

## Solution

```csharp
using System.Collections.Generic;

public class Solution {
    public int[][] Insert(int[][] intervals, int[] newInterval) {
        var result = new List<int[]>();
        int i = 0, n = intervals.Length;
        // Add all intervals before newInterval
        while (i < n && intervals[i][1] < newInterval[0]) {
            result.Add(intervals[i++]);
        }
        // Merge overlapping intervals
        while (i < n && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = System.Math.Min(newInterval[0], intervals[i][0]);
            newInterval[1] = System.Math.Max(newInterval[1], intervals[i][1]);
            i++;
        }
        result.Add(newInterval);
        // Add the rest
        while (i < n) {
            result.Add(intervals[i++]);
        }
        return result.ToArray();
    }
}
```