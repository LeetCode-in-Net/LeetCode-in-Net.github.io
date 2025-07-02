[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 30\. Substring with Concatenation of All Words

Hard

You are given a string `s` and an array of strings `words` of **the same length**. Return all starting indices of substring(s) in `s` that is a concatenation of each word in `words` **exactly once**, **in any order**, and **without any intervening characters**.

You can return the answer in **any order**.

**Example 1:**

**Input:** s = "barfoothefoobarman", words = ["foo","bar"]

**Output:** [0,9]

**Explanation:** Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively. The output order does not matter, returning [9,0] is fine too. 

**Example 2:**

**Input:** s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]

**Output:** [] 

**Example 3:**

**Input:** s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]

**Output:** [6,9,12] 

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of lower-case English letters.
*   `1 <= words.length <= 5000`
*   `1 <= words[i].length <= 30`
*   `words[i]` consists of lower-case English letters.

## Solution

```csharp
public class Solution {
    public IList<int> FindSubstring(string s, string[] words) {
        var res = new List<int>();
        if (string.IsNullOrEmpty(s) || words == null || words.Length == 0) {
            return res;
        }
        int wordLen = words[0].Length;
        int numWords = words.Length;
        int totalLen = wordLen * numWords;
        if (s.Length < totalLen) {
            return res;
        }
        var wordCount = new Dictionary<string, int>();
        foreach (var word in words) {
            if (wordCount.ContainsKey(word)) {
                wordCount[word]++;
            } else {
                wordCount[word] = 1;
            }
        }
        for (int i = 0; i < wordLen; i++) {
            int left = i;
            int count = 0;
            var seenWords = new Dictionary<string, int>();
            for (int j = i; j <= s.Length - wordLen; j += wordLen) {
                string word = s.Substring(j, wordLen);
                if (wordCount.ContainsKey(word)) {
                    if (seenWords.ContainsKey(word)) {
                        seenWords[word]++;
                    } else {
                        seenWords[word] = 1;
                    }
                    if (seenWords[word] <= wordCount[word]) {
                        count++;
                    } else {
                        while (seenWords[word] > wordCount[word]) {
                            string leftWord = s.Substring(left, wordLen);
                            seenWords[leftWord]--;
                            if (seenWords[leftWord] < wordCount[leftWord]) {
                                count--;
                            }
                            left += wordLen;
                        }
                    }
                    if (count == numWords) {
                        res.Add(left);
                        string leftWord = s.Substring(left, wordLen);
                        seenWords[leftWord]--;
                        count--;
                        left += wordLen;
                    }
                } else {
                    seenWords.Clear();
                    count = 0;
                    left = j + wordLen;
                }
            }
        }
        return res;
    }
}
}
```