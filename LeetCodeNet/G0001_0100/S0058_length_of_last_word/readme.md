[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 58\. Length of Last Word

Easy

Given a string `s` consisting of some words separated by some number of spaces, return _the length of the **last** word in the string._

A **word** is a maximal substring consisting of non-space characters only.

**Example 1:**

**Input:** s = "Hello World"

**Output:** 5

**Explanation:** The last word is "World" with length 5. 

**Example 2:**

**Input:** s = " fly me to the moon "

**Output:** 4

**Explanation:** The last word is "moon" with length 4. 

**Example 3:**

**Input:** s = "luffy is still joyboy"

**Output:** 6

**Explanation:** The last word is "joyboy" with length 6. 

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of only English letters and spaces `' '`.
*   There will be at least one word in `s`.

## Solution

```csharp
public class Solution {
    public int LengthOfLastWord(string s) {
        int len = 0;
        for (int i = s.Length - 1; i >= 0; i--) {
            char ch = s[i];
            if (ch == ' ' && len > 0) {
                break;
            } else if (ch != ' ') {
                len++;
            }
        }
        return len;
    }
}
```