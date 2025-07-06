[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 61\. Rotate List

Medium

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

**Input:** head = [1,2,3,4,5], k = 2

**Output:** [4,5,1,2,3] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

**Input:** head = [0,1,2], k = 4

**Output:** [2,0,1] 

**Constraints:**

*   The number of nodes in the list is in the range `[0, 500]`.
*   `-100 <= Node.val <= 100`
*   <code>0 <= k <= 2 * 10<sup>9</sup></code>

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
    public ListNode RotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0) {
            return head;
        }
        // Compute the length
        int len = 1;
        ListNode tail = head;
        while (tail.next != null) {
            tail = tail.next;
            len++;
        }
        k = k % len;
        if (k == 0) {
            return head;
        }
        // Make it a circle
        tail.next = head;
        // Find new tail: (len - k - 1)th node
        ListNode newTail = head;
        for (int i = 0; i < len - k - 1; i++) {
            newTail = newTail.next;
        }
        ListNode newHead = newTail.next;
        newTail.next = null;
        return newHead;
    }
}
```