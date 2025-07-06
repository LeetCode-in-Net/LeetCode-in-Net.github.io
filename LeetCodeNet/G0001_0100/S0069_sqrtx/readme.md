[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 69\. Sqrt(x)

Easy

Given a non-negative integer `x`, compute and return _the square root of_ `x`.

Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.

**Note:** You are not allowed to use any built-in exponent function or operator, such as `pow(x, 0.5)` or `x ** 0.5`.

**Example 1:**

**Input:** x = 4

**Output:** 2 

**Example 2:**

**Input:** x = 8

**Output:** 2

**Explanation:** The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.

**Constraints:**

*   <code>0 <= x <= 2<sup>31</sup> - 1</code>

## Solution

```csharp
public class Solution {
    public int MySqrt(int x) {
        if (x < 2) {
            return x;
        }
        int left = 1;
        int right = x / 2;
        int ans = 0;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if ((long)mid * mid == x) {
                return mid;
            }
            if ((long)mid * mid < x) {
                ans = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return ans;
    }
}
```