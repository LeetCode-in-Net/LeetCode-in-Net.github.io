[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 209\. Minimum Size Subarray Sum

Medium

Given an array of positive integers `nums` and a positive integer `target`, return the minimal length of a **contiguous subarray** <code>[nums<sub>l</sub>, nums<sub>l+1</sub>, ..., nums<sub>r-1</sub>, nums<sub>r</sub>]</code> of which the sum is greater than or equal to `target`. If there is no such subarray, return `0` instead.

**Example 1:**

**Input:** target = 7, nums = [2,3,1,2,4,3]

**Output:** 2

**Explanation:** The subarray [4,3] has the minimal length under the problem constraint. 

**Example 2:**

**Input:** target = 4, nums = [1,4,4]

**Output:** 1 

**Example 3:**

**Input:** target = 11, nums = [1,1,1,1,1,1,1,1]

**Output:** 0 

**Constraints:**

*   <code>1 <= target <= 10<sup>9</sup></code>
*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>1 <= nums[i] <= 10<sup>5</sup></code>

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution of which the time complexity is `O(n log(n))`.

## Solution

```csharp
public class Solution {
    public int MinSubArrayLen(int target, int[] nums) {
        int i = 0, j = 0, sum = 0, min = int.MaxValue;
        while (j < nums.Length) {
            sum += nums[j];
            if (sum >= target) {
                while (i <= j) {
                    if (sum - nums[i] >= target) {
                        sum -= nums[i];
                        i++;
                    } else {
                        break;
                    }
                }
                if (j - i + 1 < min) {
                    min = j - i + 1;
                }
            }
            j++;
        }
        return min == int.MaxValue ? 0 : min;
    }
}
```