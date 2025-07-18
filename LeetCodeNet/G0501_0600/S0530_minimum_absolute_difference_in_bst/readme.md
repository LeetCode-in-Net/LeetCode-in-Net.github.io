[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 530\. Minimum Absolute Difference in BST

Easy

Given the `root` of a Binary Search Tree (BST), return _the minimum absolute difference between the values of any two different nodes in the tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/05/bst1.jpg)

**Input:** root = [4,2,6,1,3]

**Output:** 1

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/05/bst2.jpg)

**Input:** root = [1,0,48,null,null,12,49]

**Output:** 1

**Constraints:**

*   The number of nodes in the tree is in the range <code>[2, 10<sup>4</sup>]</code>.
*   <code>0 <= Node.val <= 10<sup>5</sup></code>

**Note:** This question is the same as 783: [https://leetcode.com/problems/minimum-distance-between-bst-nodes/](https://leetcode.com/problems/minimum-distance-between-bst-nodes/)

## Solution

```csharp
using System;
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
    private int ans = int.MaxValue;
    private int? prev = null;

    public int GetMinimumDifference(TreeNode root) {
        InOrder(root);
        return ans;
    }
    
    private void InOrder(TreeNode node) {
        if (node == null) {
            return;
        }
        InOrder(node.left);
        if (prev != null) {
            ans = Math.Min(ans, Math.Abs((int) node.val - prev.Value));
        }
        prev = node.val;
        InOrder(node.right);
    }
}
```