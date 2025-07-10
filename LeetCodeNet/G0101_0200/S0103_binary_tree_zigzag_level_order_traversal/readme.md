[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 103\. Binary Tree Zigzag Level Order Traversal

Medium

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** [[3],[20,9],[15,7]] 

**Example 2:**

**Input:** root = [1]

**Output:** [[1]] 

**Example 3:**

**Input:** root = []

**Output:** [] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-100 <= Node.val <= 100`

## Solution

```csharp
using System.Collections.Generic;
using LeetCodeNet.Com_github_leetcode;

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public IList<IList<int>> ZigzagLevelOrder(TreeNode root) {
        var queue = new Queue<TreeNode>();
        var results = new List<IList<int>>();
        if (root == null) {
            return results;
        }
        var level = new List<int>();
        queue.Enqueue(root);
        queue.Enqueue(null);
        var d = false;
        while (queue.Count > 0) {
            var c = queue.Dequeue();
            if (c == null) {
                if (d) {
                    level.Reverse();
                }
                results.Add(level);
                if (queue.Count == 0) {
                    break;
                } else {
                    queue.Enqueue(null);
                    level = new List<int>();
                    d = !d;
                }
            } else {
                level.Add((int)c.val);
                if (c.left != null) {
                    queue.Enqueue(c.left);
                }
                if (c.right != null) {
                    queue.Enqueue(c.right);
                }
            }
        }
        return results;
    }
}
```