[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 383\. Ransom Note

Easy

Given two stings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed from `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

**Example 1:**

**Input:** ransomNote = "a", magazine = "b"

**Output:** false

**Example 2:**

**Input:** ransomNote = "aa", magazine = "ab"

**Output:** false

**Example 3:**

**Input:** ransomNote = "aa", magazine = "aab"

**Output:** true

**Constraints:**

*   <code>1 <= ransomNote.length, magazine.length <= 10<sup>5</sup></code>
*   `ransomNote` and `magazine` consist of lowercase English letters.

## Solution

```csharp
public class Solution {
    public bool CanConstruct(string ransomNote, string magazine) {
        int[] count = new int[26];
        foreach (char c in magazine) count[c - 'a']++;
        foreach (char c in ransomNote) {
            if (--count[c - 'a'] < 0) return false;
        }
        return true;
    }
}
```