[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 201\. Bitwise AND of Numbers Range

Medium

Given two integers `left` and `right` that represent the range `[left, right]`, return _the bitwise AND of all numbers in this range, inclusive_.

**Example 1:**

**Input:** left = 5, right = 7

**Output:** 4 

**Example 2:**

**Input:** left = 0, right = 0

**Output:** 0 

**Example 3:**

**Input:** left = 1, right = 2147483647

**Output:** 0 

**Constraints:**

*   <code>0 <= left <= right <= 2<sup>31</sup> - 1</code>

## Solution

```csharp
public class Solution {
    public int RangeBitwiseAnd(int left, int right) {
        var shift = 0;
        for (; left != right; left >>= 1, right >>= 1, shift++) { 

        }
        return left << shift;
    }
}
```