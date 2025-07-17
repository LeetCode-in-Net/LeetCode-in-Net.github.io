[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 290\. Word Pattern

Easy

Given a `pattern` and a string `s`, find if `s` follows the same pattern.

Here **follow** means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** word in `s`.

**Example 1:**

**Input:** pattern = "abba", s = "dog cat cat dog"

**Output:** true 

**Example 2:**

**Input:** pattern = "abba", s = "dog cat cat fish"

**Output:** false 

**Example 3:**

**Input:** pattern = "aaaa", s = "dog cat cat dog"

**Output:** false 

**Example 4:**

**Input:** pattern = "abba", s = "dog dog dog dog"

**Output:** false 

**Constraints:**

*   `1 <= pattern.length <= 300`
*   `pattern` contains only lower-case English letters.
*   `1 <= s.length <= 3000`
*   `s` contains only lower-case English letters and spaces `' '`.
*   `s` **does not contain** any leading or trailing spaces.
*   All the words in `s` are separated by a **single space**.

## Solution

```csharp
public class Solution {
    public bool WordPattern(string pattern, string s) {
        Dictionary<char, string> dict = new();
        string[] str = s.Split(" ");
        if (pattern.Length != str.Length) {
            return false;
        }
        for (int i = 0; i < pattern.Length; i++) {
            if (!dict.ContainsKey(pattern[i]) && !dict.ContainsValue(str[i])) {
                dict.Add(pattern[i], str[i]);
            }
            if (!dict.ContainsKey(pattern[i]) || !str[i].Equals(dict[pattern[i]])) {
                return false;
            }
        }
        return true;
    }
}
```