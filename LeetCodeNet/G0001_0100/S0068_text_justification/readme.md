[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 68\. Text Justification

Hard

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified and no extra space is inserted between words.

**Note:**

*   A word is defined as a character sequence consisting of non-space characters only.
*   Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
*   The input array `words` contains at least one word.

**Example 1:**

**Input:** words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16

**Output:** [ "This is an", "example of text", "justification. " ]

**Example 2:**

**Input:** words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16

**Output:** [ "What must be", "acknowledgment ", "shall be " ]

**Explanation:** Note that the last line is "shall be " instead of "shall be", because the last line must be left-justified instead of fully-justified. Note that the second line is also left-justified becase it contains only one word.

**Example 3:**

**Input:** words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20

**Output:** [ "Science is what we", "understand well", "enough to explain to", "a computer. Art is", "everything else we", "do " ]

**Constraints:**

*   `1 <= words.length <= 300`
*   `1 <= words[i].length <= 20`
*   `words[i]` consists of only English letters and symbols.
*   `1 <= maxWidth <= 100`
*   `words[i].length <= maxWidth`

## Solution

```csharp
public class Solution {
    public IList<string> FullJustify(string[] words, int maxWidth) {
        var res = new List<string>();
        int i = 0;
        int n = words.Length;
        while (i < n) {
            int j = i, lineLen = 0;
            while (j < n && lineLen + words[j].Length + (j - i) <= maxWidth) {
                lineLen += words[j].Length;
                j++;
            }
            int spaces = maxWidth - lineLen;
            int gaps = j - i - 1;
            var line = new System.Text.StringBuilder();
            if (j == n || gaps == 0) {
                for (int k = i; k < j; k++) {
                    line.Append(words[k]);
                    if (k < j - 1) {
                        line.Append(' ');
                    }
                }
                line.Append(' ', maxWidth - line.Length);
            } else {
                int spaceEach = spaces / gaps;
                int extra = spaces % gaps;
                for (int k = i; k < j; k++) {
                    line.Append(words[k]);
                    if (k < j - 1) {
                        line.Append(' ', spaceEach + (k - i < extra ? 1 : 0));
                    }
                }
            }
            res.Add(line.ToString());
            i = j;
        }
        return res;
    }
}
```