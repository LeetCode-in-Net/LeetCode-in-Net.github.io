[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 14\. Longest Common Prefix

Easy

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

**Input:** strs = ["flower","flow","flight"]

**Output:** "fl" 

**Example 2:**

**Input:** strs = ["dog","racecar","car"]

**Output:** ""

**Explanation:** There is no common prefix among the input strings. 

**Constraints:**

*   `1 <= strs.length <= 200`
*   `0 <= strs[i].length <= 200`
*   `strs[i]` consists of only lower-case English letters.

## Solution

```csharp
public class Solution {
    public string LongestCommonPrefix(string[] strs) {
        if (strs.Length < 1) {
            return "";
        }
        if (strs.Length == 1) {
            return strs[0];
        }
        string temp = strs[0];
        int i = 1;
        string cur;
        while (!string.IsNullOrEmpty(temp) && i < strs.Length) {
            if (temp.Length > strs[i].Length) {
                temp = temp.Substring(0, strs[i].Length);
            }
            cur = strs[i].Substring(0, temp.Length);
            if (!cur.Equals(temp)) {
                temp = temp.Substring(0, temp.Length - 1);
            } else {
                i++;
            }
        }
        return temp;
    }
}
```