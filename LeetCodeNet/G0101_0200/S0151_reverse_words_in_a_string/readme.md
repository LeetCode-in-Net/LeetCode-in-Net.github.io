[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 151\. Reverse Words in a String

Medium

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return _a string of the words in reverse order concatenated by a single space._

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1:**

**Input:** s = "the sky is blue"

**Output:** "blue is sky the" 

**Example 2:**

**Input:** s = " hello world "

**Output:** "world hello"

**Explanation:** Your reversed string should not contain leading or trailing spaces. 

**Example 3:**

**Input:** s = "a good example"

**Output:** "example good a"

**Explanation:** You need to reduce multiple spaces between two words to a single space in the reversed string. 

**Example 4:**

**Input:** s = " Bob Loves Alice "

**Output:** "Alice Loves Bob" 

**Example 5:**

**Input:** s = "Alice does not even like bob"

**Output:** "bob like even not does Alice" 

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
*   There is **at least one** word in `s`.

**Follow-up:** If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?

## Solution

```csharp
using System.Text;

public class Solution {
    public string ReverseWords(string s) {
        var sb = new StringBuilder();
        int i = s.Length - 1;
        while (i >= 0) {
            if (s[i] == ' ') {
                i--;
                continue;
            }
            int start = s.LastIndexOf(' ', i);
            sb.Append(' ');
            sb.Append(s, start + 1, i - start);
            i = start - 1;
        }
        if (sb.Length > 0) {
            sb.Remove(0, 1);
        }
        return sb.ToString();
    }
}
```