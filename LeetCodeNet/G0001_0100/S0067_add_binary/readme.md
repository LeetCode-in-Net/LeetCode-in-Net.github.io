[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 67\. Add Binary

Easy

Given two binary strings `a` and `b`, return _their sum as a binary string_.

**Example 1:**

**Input:** a = "11", b = "1"

**Output:** "100" 

**Example 2:**

**Input:** a = "1010", b = "1011"

**Output:** "10101" 

**Constraints:**

*   <code>1 <= a.length, b.length <= 10<sup>4</sup></code>
*   `a` and `b` consist only of `'0'` or `'1'` characters.
*   Each string does not contain leading zeros except for the zero itself.

## Solution

```csharp
public class Solution {
    public string AddBinary(string a, string b) {
        var sb = new System.Text.StringBuilder();
        int i = a.Length - 1; 
        int j = b.Length - 1; 
        int carry = 0;
        while (i >= 0 || j >= 0 || carry > 0) {
            int sum = carry;
            if (i >= 0) {
                sum += a[i--] - '0';
            }
            if (j >= 0) {
                sum += b[j--] - '0';
            }
            sb.Insert(0, (char)('0' + (sum % 2)));
            carry = sum / 2;
        }
        return sb.ToString();
    }
}
```