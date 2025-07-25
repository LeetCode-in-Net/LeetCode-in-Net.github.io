[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 128\. Longest Consecutive Sequence

Medium

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]

**Output:** 4

**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4. 

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]

**Output:** 9 

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

## Solution

```csharp
public class Solution {
    public int LongestConsecutive(int[] nums) {
        Dictionary<int, int> mapToHighest = new(nums.Length);
        int best = 0;
        for (int i = 0; i < nums.Length; i++) {
            int rangeLow = 0;
            int rangeHigh = 0;
            if (mapToHighest.ContainsKey(nums[i])) {
                continue;
            }
            if (mapToHighest.TryGetValue(nums[i]-1, out var downCount)) {
                rangeLow = downCount;
            }
            if (mapToHighest.TryGetValue(nums[i]+1, out var upCount)) {
                rangeHigh = upCount;
            }
            int thisSum = rangeLow + rangeHigh + 1;
            mapToHighest[nums[i] - rangeLow] = thisSum;
            mapToHighest[nums[i] + rangeHigh] = thisSum;
            if (rangeLow != 0 && rangeHigh != 0) {
                mapToHighest[nums[i]] = 1;
            }
            best = Math.Max(thisSum, best);
        }
        return best;
    }
}
```