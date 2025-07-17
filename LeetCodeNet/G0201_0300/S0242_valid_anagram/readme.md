[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 242\. Valid Anagram

Easy

Given two strings `s` and `t`, return `true` _if_ `t` _is an anagram of_ `s`_, and_ `false` _otherwise_.

**Example 1:**

**Input:** s = "anagram", t = "nagaram"

**Output:** true 

**Example 2:**

**Input:** s = "rat", t = "car"

**Output:** false 

**Constraints:**

*   <code>1 <= s.length, t.length <= 5 * 10<sup>4</sup></code>
*   `s` and `t` consist of lowercase English letters.

**Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

## Solution

```csharp
public class Solution {
    public bool IsAnagram(string s, string t) {
        if (s.Length != t.Length) {
            return false;
        }
        int[] charFreqMap = new int[26];
        foreach (char c in s) {
            charFreqMap[c - 'a']++;
        }
        foreach (char c in t) {
            if (charFreqMap[c - 'a'] == 0) {
                return false;
            }
            charFreqMap[c - 'a']--;
        }
        return true;
    }
}
```