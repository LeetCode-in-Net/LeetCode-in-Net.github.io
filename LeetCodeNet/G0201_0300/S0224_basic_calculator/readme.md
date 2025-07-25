[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 224\. Basic Calculator

Hard

Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return _the result of the evaluation_.

**Note:** You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Example 1:**

**Input:** s = "1 + 1"

**Output:** 2 

**Example 2:**

**Input:** s = " 2-1 + 2 "

**Output:** 3 

**Example 3:**

**Input:** s = "(1+(4+5+2)-3)+(6+8)"

**Output:** 23 

**Constraints:**

*   <code>1 <= s.length <= 3 * 10<sup>5</sup></code>
*   `s` consists of digits, `'+'`, `'-'`, `'('`, `')'`, and `' '`.
*   `s` represents a valid expression.
*   `'+'` is **not** used as a unary operation (i.e., `"+1"` and `"+(2 + 3)"` is invalid).
*   `'-'` could be used as a unary operation (i.e., `"-1"` and `"-(2 + 3)"` is valid).
*   There will be no two consecutive operators in the input.
*   Every number and running calculation will fit in a signed 32-bit integer.

## Solution

```csharp
public class Solution {
    public int Calculate(string s) {
        Stack<int> st = new Stack<int>();
        int ans = 0;
        int sum = 0;
        int sign = 1;
        st.Push(1);
        foreach (char ch in s) {
            if (ch >= '0' && ch <= '9') {
                sum = sum * 10 + ch - '0';
            } else if (ch == '(') {
                st.Push(sign);
            } else if (ch == ')') {
                st.Pop();
            } else if (ch == '-' || ch == '+') {
                ans += sum * sign;
                if (ch == '-') {
                    sign = -1 * st.Peek();
                } else {
                    sign = st.Peek();
                }
                sum = 0;
            }
        }
        ans += sum * sign;
        return ans;
    }
}
```