[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 127\. Word Ladder

Hard

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words <code>beginWord -> s<sub>1</sub> -> s<sub>2</sub> -> ... -> s<sub>k</sub></code> such that:

*   Every adjacent pair of words differs by a single letter.
*   Every <code>s<sub>i</sub></code> for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
*   <code>s<sub>k</sub> == endWord</code>

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return _the **number of words** in the **shortest transformation sequence** from_ `beginWord` _to_ `endWord`_, or_ `0` _if no such sequence exists._

**Example 1:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]

**Output:** 5

**Explanation:** One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long. 

**Example 2:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]

**Output:** 0

**Explanation:** The endWord "cog" is not in wordList, therefore there is no valid transformation sequence. 

**Constraints:**

*   `1 <= beginWord.length <= 10`
*   `endWord.length == beginWord.length`
*   `1 <= wordList.length <= 5000`
*   `wordList[i].length == beginWord.length`
*   `beginWord`, `endWord`, and `wordList[i]` consist of lowercase English letters.
*   `beginWord != endWord`
*   All the words in `wordList` are **unique**.

## Solution

```csharp
using System.Collections.Generic;

public class Solution {
    public int LadderLength(string beginWord, string endWord, IList<string> wordDict) {
        var beginSet = new HashSet<string>();
        var endSet = new HashSet<string>();
        var wordSet = new HashSet<string>(wordDict);
        var visited = new HashSet<string>();
        if (!wordDict.Contains(endWord)) {
            return 0;
        }
        int len = 1;
        int strLen = beginWord.Length;
        beginSet.Add(beginWord);
        endSet.Add(endWord);
        while (beginSet.Count > 0 && endSet.Count > 0) {
            if (beginSet.Count > endSet.Count) {
                var temp = beginSet;
                beginSet = endSet;
                endSet = temp;
            }
            var tempSet = new HashSet<string>();
            foreach (var s in beginSet) {
                char[] chars = s.ToCharArray();
                for (int i = 0; i < strLen; i++) {
                    char old = chars[i];
                    for (char j = 'a'; j <= 'z'; j++) {
                        chars[i] = j;
                        string temp = new string(chars);
                        if (endSet.Contains(temp)) {
                            return len + 1;
                        }
                        if (!visited.Contains(temp) && wordSet.Contains(temp)) {
                            tempSet.Add(temp);
                            visited.Add(temp);
                        }
                    }
                    chars[i] = old;
                }
            }
            beginSet = tempSet;
            len++;
        }
        return 0;
    }
}
```