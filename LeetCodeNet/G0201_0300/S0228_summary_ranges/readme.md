[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 228\. Summary Ranges

Easy

You are given a **sorted unique** integer array `nums`.

Return _the **smallest sorted** list of ranges that **cover all the numbers in the array exactly**_. That is, each element of `nums` is covered by exactly one of the ranges, and there is no integer `x` such that `x` is in one of the ranges but not in `nums`.

Each range `[a,b]` in the list should be output as:

*   `"a->b"` if `a != b`
*   `"a"` if `a == b`

**Example 1:**

**Input:** nums = [0,1,2,4,5,7]

**Output:** ["0->2","4->5","7"]

**Explanation:** The ranges are: [0,2] --> "0->2" [4,5] --> "4->5" [7,7] --> "7" 

**Example 2:**

**Input:** nums = [0,2,3,4,6,8,9]

**Output:** ["0","2->4","6","8->9"]

**Explanation:** The ranges are: [0,0] --> "0" [2,4] --> "2->4" [6,6] --> "6" [8,9] --> "8->9" 

**Example 3:**

**Input:** nums = []

**Output:** [] 

**Example 4:**

**Input:** nums = [-1]

**Output:** ["-1"] 

**Example 5:**

**Input:** nums = [0]

**Output:** ["0"] 

**Constraints:**

*   `0 <= nums.length <= 20`
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>
*   All the values of `nums` are **unique**.
*   `nums` is sorted in ascending order.

## Solution

```csharp
public class Solution {
    public IList<string> SummaryRanges(int[] nums) {
        List<string> result = new List<string>();
        if (nums.Length == 0) {
            return result;
        }
        int startIndex = 0;
        for (int i = 1; i < nums.Length; ++i) {
            if (nums[i] != nums[i - 1] + 1) {
                if (startIndex != i - 1) {
                    result.Add(nums[startIndex] + "->" + (nums[i - 1]).ToString());
                } else {
                    result.Add(nums[startIndex].ToString());
                }
                startIndex = i;
            }
        }
        if (startIndex != nums.Length - 1) {
            result.Add(nums[startIndex] + "->" + (nums[nums.Length - 1]).ToString());
        } else {
            result.Add(nums[startIndex].ToString());
        }
        return result;
    }
}
```