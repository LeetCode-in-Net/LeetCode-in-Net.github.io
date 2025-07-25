[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 172\. Factorial Trailing Zeroes

Medium

Given an integer `n`, return _the number of trailing zeroes in_ `n!`.

Note that `n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1`.

**Example 1:**

**Input:** n = 3

**Output:** 0

**Explanation:** 3! = 6, no trailing zero. 

**Example 2:**

**Input:** n = 5

**Output:** 1

**Explanation:** 5! = 120, one trailing zero. 

**Example 3:**

**Input:** n = 0

**Output:** 0 

**Constraints:**

*   <code>0 <= n <= 10<sup>4</sup></code>

**Follow up:** Could you write a solution that works in logarithmic time complexity?

## Solution

```csharp
public class Solution {
    public int TrailingZeroes(int n) {
        int baseN = 5;
        int count = 0;
        while (n >= baseN) {
            count += n / baseN;
            baseN = baseN * 5;
        }
        return count;
    }
}
```