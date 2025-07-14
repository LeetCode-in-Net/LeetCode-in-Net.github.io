[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 212\. Word Search II

Hard

Given an `m x n` `board` of characters and a list of strings `words`, return _all words on the board_.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)

**Input:** board = \[\["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]

**Output:** ["eat","oath"] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg)

**Input:** board = \[\["a","b"],["c","d"]], words = ["abcb"]

**Output:** [] 

**Constraints:**

*   `m == board.length`
*   `n == board[i].length`
*   `1 <= m, n <= 12`
*   `board[i][j]` is a lowercase English letter.
*   <code>1 <= words.length <= 3 * 10<sup>4</sup></code>
*   `1 <= words[i].length <= 10`
*   `words[i]` consists of lowercase English letters.
*   All the strings of `words` are unique.

## Solution

```csharp
using System.Collections.Generic;

public class Solution {
    private Tree root;

    public IList<string> FindWords(char[][] board, string[] words) {
        if (board.Length < 1 || board[0].Length < 1) {
            return new List<string>();
        }
        root = new Tree();
        foreach (var word in words) {
            Tree.AddWord(root, word);
        }
        var collected = new List<string>();
        for (int i = 0; i < board.Length; ++i) {
            for (int j = 0; j < board[0].Length; ++j) {
                Dfs(board, i, j, root, collected);
            }
        }
        return collected;
    }

    private void Dfs(char[][] board, int i, int j, Tree cur, List<string> collected) {
        char c = board[i][j];
        if (c == '-') {
            return;
        }
        cur = cur.GetChild(c);
        if (cur == null) {
            return;
        }
        if (cur.end != null) {
            string s = cur.end;
            collected.Add(s);
            cur.end = null;
            if (cur.Len() == 0) {
                Tree.DeleteWord(root, s);
            }
        }
        board[i][j] = '-';
        if (i > 0) {
            Dfs(board, i - 1, j, cur, collected);
        }
        if (i + 1 < board.Length) {
            Dfs(board, i + 1, j, cur, collected);
        }
        if (j > 0) {
            Dfs(board, i, j - 1, cur, collected);
        }
        if (j + 1 < board[0].Length) {
            Dfs(board, i, j + 1, cur, collected);
        }
        board[i][j] = c;
    }

    // Internal Trie/Tree class
    private class Tree {
        private readonly Tree[] children = new Tree[26];
        public string? end;

        public Tree GetChild(char c) {
            return children[c - 'a'];
        }

        public int Len() {
            int count = 0;
            foreach (var child in children) {
                if (child != null) {
                    count++;
                }
            }
            return count;
        }

        public static void AddWord(Tree root, string word) {
            var node = root;
            foreach (var c in word) {
                int idx = c - 'a';
                if (node.children[idx] == null) {
                    node.children[idx] = new Tree();
                }
                node = node.children[idx];
            }
            node.end = word;
        }

        public static void DeleteWord(Tree root, string word) {
            DeleteWordHelper(root, word, 0);
        }

        private static bool DeleteWordHelper(Tree node, string word, int d) {
            if (node == null) {
                return false;
            }
            if (d == word.Length) {
                node.end = null;
            }
            else {
                int idx = word[d] - 'a';
                if (DeleteWordHelper(node.children[idx], word, d + 1)) {
                    node.children[idx] = null;
                }
            }
            if (node.end != null) {
                return false;
            }
            foreach (var child in node.children) {
                if (child != null) return false;
            }
            return true;
        }
    }
}
```