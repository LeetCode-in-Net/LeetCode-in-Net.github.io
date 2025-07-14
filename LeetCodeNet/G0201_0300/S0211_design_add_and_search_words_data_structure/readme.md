[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 211\. Design Add and Search Words Data Structure

Medium

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

*   `WordDictionary()` Initializes the object.
*   `void addWord(word)` Adds `word` to the data structure, it can be matched later.
*   `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

**Example:**

**Input**

    ["WordDictionary","addWord","addWord","addWord","search","search","search","search"] [[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
    
**Output**

    [null,null,null,null,false,true,true,true]

**Explanation**

    WordDictionary wordDictionary = new WordDictionary();
    wordDictionary.addWord("bad");
    wordDictionary.addWord("dad");
    wordDictionary.addWord("mad");
    wordDictionary.search("pad"); // return False
    wordDictionary.search("bad"); // return True
    wordDictionary.search(".ad"); // return True
    wordDictionary.search("b.."); // return True 

**Constraints:**

*   `1 <= word.length <= 500`
*   `word` in `addWord` consists lower-case English letters.
*   `word` in `search` consist of `'.'` or lower-case English letters.
*   At most `50000` calls will be made to `addWord` and `search`.

## Solution

```csharp
public class WordDictionary {
    private class Node {
        public Node[] kids = new Node[26];
        public bool isTerminal;
    }

    private readonly Node[] root = new Node[26];

    public WordDictionary() {
        // empty constructor
    }

    public void AddWord(string word) {
        int n = word.Length;
        if (root[n] == null) {
            root[n] = new Node();
        }
        Node node = root[n];
        for (int i = 0; i < n; i++) {
            int c = word[i] - 'a';
            Node kid = node.kids[c];
            if (kid == null) {
                kid = new Node();
                node.kids[c] = kid;
            }
            node = kid;
        }
        node.isTerminal = true;
    }

    public bool Search(string word) {
        Node node = root[word.Length];
        return node != null && Dfs(0, node, word);
    }

    private bool Dfs(int i, Node node, string word) {
        int len = word.Length;
        if (i == len) {
            return false;
        }
        char c = word[i];
        if (c == '.') {
            foreach (Node kid in node.kids) {
                if (kid == null) {
                    continue;
                }
                if ((i == len - 1 && kid.isTerminal) || Dfs(i + 1, kid, word)) {
                    return true;
                }
            }
            return false;
        }
        Node next = node.kids[c - 'a'];
        if (next == null) {
            return false;
        }
        if (i == len - 1) {
            return next.isTerminal;
        }
        return Dfs(i + 1, next, word);
    }
}
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.AddWord(word);
 */
```