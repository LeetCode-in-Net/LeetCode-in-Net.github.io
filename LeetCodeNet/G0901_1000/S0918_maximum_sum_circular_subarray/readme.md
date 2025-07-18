[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 918\. Maximum Sum Circular Subarray

Medium

Given a **circular integer array** `nums` of length `n`, return _the maximum possible sum of a non-empty **subarray** of_ `nums`.

A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A **subarray** may only include each element of the fixed buffer `nums` at most once. Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i <= k1`, `k2 <= j` with `k1 % n == k2 % n`.

**Example 1:**

**Input:** nums = [1,-2,3,-2]

**Output:** 3

**Explanation:** Subarray [3] has maximum sum 3. 

**Example 2:**

**Input:** nums = [5,-3,5]

**Output:** 10

**Explanation:** Subarray [5,5] has maximum sum 5 + 5 = 10. 

**Example 3:**

**Input:** nums = [-3,-2,-3]

**Output:** -2

**Explanation:** Subarray [-2] has maximum sum -2. 

**Constraints:**

*   `n == nums.length`
*   <code>1 <= n <= 3 * 10<sup>4</sup></code>
*   <code>-3 * 10<sup>4</sup> <= nums[i] <= 3 * 10<sup>4</sup></code>

## Solution

```csharp
using System;
using System.Linq;

public class Solution {
    private int Kadane(int[] nums, int sign) {
        int currSum = int.MinValue;
        int maxSum = int.MinValue;
        foreach (int i in nums) {
            currSum = sign * i + Math.Max(currSum, 0);
            maxSum = Math.Max(maxSum, currSum);
        }
        return maxSum;
    }

    public int MaxSubarraySumCircular(int[] nums) {
        if (nums.Length == 1) {
            return nums[0];
        }
        int sumOfArray = 0;
        foreach (int i in nums) {
            sumOfArray += i;
        }
        int maxSumSubarray = Kadane(nums, 1);
        int minSumSubarray = Kadane(nums, -1) * -1;
        // If all numbers are negative, minSumSubarray will be sumOfArray.
        // In this case, the circular sum (sumOfArray - minSumSubarray) would be 0,
        // which is incorrect if the actual answer is the largest negative number.
        // The largest negative number would be captured by maxSumSubarray.
        if (sumOfArray == minSumSubarray) {
            return maxSumSubarray;
        } else {
            return Math.Max(maxSumSubarray, sumOfArray - minSumSubarray);
        }
    }
}
```