[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 21\. Merge Two Sorted Lists

Easy

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**Input:** l1 = [1,2,4], l2 = [1,3,4]

**Output:** [1,1,2,3,4,4] 

**Example 2:**

**Input:** l1 = [], l2 = []

**Output:** [] 

**Example 3:**

**Input:** l1 = [], l2 = [0]

**Output:** [0] 

**Constraints:**

*   The number of nodes in both lists is in the range `[0, 50]`.
*   `-100 <= Node.val <= 100`
*   Both `l1` and `l2` are sorted in **non-decreasing** order.

## Solution

```csharp
using LeetCodeNet.Com_github_leetcode;

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode MergeTwoLists(ListNode l1, ListNode l2) {
        ListNode list = new ListNode(-1);
        ListNode head = list;
        while (l1 != null || l2 != null) {
            if (l1 != null && l2 != null) {
                if (l1.val <= l2.val) {
                    list.next = new ListNode(l1.val);
                    l1 = l1.next;
                } else {
                    list.next = new ListNode(l2.val);
                    l2 = l2.next;
                }
            } else if (l1 != null) {
                list.next = new ListNode(l1.val);
                l1 = l1.next;
            } else {
                list.next = new ListNode(l2.val);
                l2 = l2.next;
            }
            list = list.next;
        }
        return head.next;
    }
}
```