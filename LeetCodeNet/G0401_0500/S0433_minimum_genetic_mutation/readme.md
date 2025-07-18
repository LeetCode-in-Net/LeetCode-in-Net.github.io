[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 433\. Minimum Genetic Mutation

Medium

A gene string can be represented by an 8-character long string, with choices from `'A'`, `'C'`, `'G'`, and `'T'`.

Suppose we need to investigate a mutation from a gene string `start` to a gene string `end` where one mutation is defined as one single character changed in the gene string.

*   For example, `"AACCGGTT" --> "AACCGGTA"` is one mutation.

There is also a gene bank `bank` that records all the valid gene mutations. A gene must be in `bank` to make it a valid gene string.

Given the two gene strings `start` and `end` and the gene bank `bank`, return _the minimum number of mutations needed to mutate from_ `start` _to_ `end`. If there is no such a mutation, return `-1`.

Note that the starting point is assumed to be valid, so it might not be included in the bank.

**Example 1:**

**Input:** start = "AACCGGTT", end = "AACCGGTA", bank = ["AACCGGTA"]

**Output:** 1 

**Example 2:**

**Input:** start = "AACCGGTT", end = "AAACGGTA", bank = ["AACCGGTA","AACCGCTA","AAACGGTA"]

**Output:** 2 

**Example 3:**

**Input:** start = "AAAAACCC", end = "AACCCCCC", bank = ["AAAACCCC","AAACCCCC","AACCCCCC"]

**Output:** 3 

**Constraints:**

*   `start.length == 8`
*   `end.length == 8`
*   `0 <= bank.length <= 10`
*   `bank[i].length == 8`
*   `start`, `end`, and `bank[i]` consist of only the characters `['A', 'C', 'G', 'T']`.

## Solution

```csharp
using System;
using System.Collections.Generic;

public class Solution {
    private IList<string> IsInBank(ISet<string> set, string cur) {
        List<string> res = new List<string>();
        foreach (string each in set) {
            int diff = 0;
            for (int i = 0; i < each.Length; i++) {
                if (each[i] != cur[i]) {
                    diff++;
                    if (diff > 1) {
                        break;
                    }
                }
            }
            if (diff == 1) {
                res.Add(each);
            }
        }
        return res;
    }

    public int MinMutation(string start, string end, string[] bank) {
        ISet<string> set = new HashSet<string>();
        foreach (string s in bank) {
            set.Add(s);
        }
        Queue<string> queue = new Queue<string>();
        queue.Enqueue(start);
        int step = 0;
        while (queue.Count > 0) {
            int curSize = queue.Count;
            while (curSize-- > 0) {
                string cur = queue.Dequeue();
                if (cur.Equals(end)) {
                    return step;
                }
                foreach (string next in IsInBank(set, cur)) {
                    queue.Enqueue(next);
                    set.Remove(next);
                }
            }
            step++;
        }
        return -1;
    }
}
```