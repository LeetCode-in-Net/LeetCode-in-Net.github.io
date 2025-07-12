[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 150\. Evaluate Reverse Polish Notation

Medium

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

**Note** that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

**Example 1:**

**Input:** tokens = ["2","1","+","3","\*"]

**Output:** 9

**Explanation:** ((2 + 1) \* 3) = 9 

**Example 2:**

**Input:** tokens = ["4","13","5","/","+"]

**Output:** 6

**Explanation:** (4 + (13 / 5)) = 6 

**Example 3:**

**Input:** tokens = ["10","6","9","3","+","-11","\*","/","\*","17","+","5","+"]

**Output:** 22

**Explanation:**

    ((10 \* (6 / ((9 + 3) \* -11))) + 17) + 5
    = ((10 \* (6 / (12 \* -11))) + 17) + 5
    = ((10 \* (6 / -132)) + 17) + 5
    = ((10 \* 0) + 17) + 5
    = (0 + 17) + 5
    = 17 + 5
    = 22 

**Constraints:**

*   <code>1 <= tokens.length <= 10<sup>4</sup></code>
*   `tokens[i]` is either an operator: `"+"`, `"-"`, `"*"`, or `"/"`, or an integer in the range `[-200, 200]`.

## Solution

```csharp
using System.Collections.Generic;

public class Solution {
    public int EvalRPN(string[] tokens) {
        var st = new Stack<int>();
        foreach (string token in tokens) {
            if (!char.IsDigit(token[token.Length - 1])) {
                int second = st.Pop();
                int first = st.Pop();
                st.Push(Eval(first, second, token));
            } else {
                st.Push(int.Parse(token));
            }
        }
        return st.Pop();
    }

    private int Eval(int first, int second, string op) {
        return op switch {
            "+" => first + second,
            "-" => first - second,
            "*" => first * second,
            _ => first / second
        };
    }
}
```