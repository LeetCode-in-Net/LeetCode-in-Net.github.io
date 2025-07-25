[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 427\. Construct Quad Tree

Medium

Given a `n * n` matrix `grid` of `0's` and `1's` only. We want to represent the `grid` with a Quad-Tree.

Return _the root of the Quad-Tree_ representing the `grid`.

Notice that you can assign the value of a node to **True** or **False** when `isLeaf` is **False**, and both are **accepted** in the answer.

A Quad-Tree is a tree data structure in which each internal node has exactly four children. Besides, each node has two attributes:

*   `val`: True if the node represents a grid of 1's or False if the node represents a grid of 0's.
*   `isLeaf`: True if the node is leaf node on the tree or False if the node has the four children.
```
    class Node {
        public boolean val;
        public boolean isLeaf;
        public Node topLeft;
        public Node topRight;
        public Node bottomLeft;
        public Node bottomRight;
    }
```
We can construct a Quad-Tree from a two-dimensional area using the following steps:

1.  If the current grid has the same value (i.e all `1's` or all `0's`) set `isLeaf` True and set `val` to the value of the grid and set the four children to Null and stop.
2.  If the current grid has different values, set `isLeaf` to False and set `val` to any value and divide the current grid into four sub-grids as shown in the photo.
3.  Recurse for each of the children with the proper sub-grid.

![](https://assets.leetcode.com/uploads/2020/02/11/new_top.png)

If you want to know more about the Quad-Tree, you can refer to the [wiki](https://en.wikipedia.org/wiki/Quadtree).

**Quad-Tree format:**

The output represents the serialized format of a Quad-Tree using level order traversal, where `null` signifies a path terminator where no node exists below.

It is very similar to the serialization of the binary tree. The only difference is that the node is represented as a list `[isLeaf, val]`.

If the value of `isLeaf` or `val` is True we represent it as **1** in the list `[isLeaf, val]` and if the value of `isLeaf` or `val` is False we represent it as **0**.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/02/11/grid1.png)

**Input:** grid = \[\[0,1],[1,0]]

**Output:** [[0,1],[1,0],[1,1],[1,1],[1,0]]

**Explanation:**

    The explanation of this example is shown below:
    Notice that 0 represnts False and 1 represents True in the photo representing the Quad-Tree.

![](https://assets.leetcode.com/uploads/2020/02/12/e1tree.png) 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/02/12/e2mat.png)

**Input:** grid = \[\[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,1,1,1,1],[1,1,1,1,1,1,1,1],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0]]

**Output:** [[0,1],[1,1],[0,1],[1,1],[1,0],null,null,null,null,[1,0],[1,0],[1,1],[1,1]]

**Explanation:**

    All values in the grid are not the same. We divide the grid into four sub-grids.
    The topLeft, bottomLeft and bottomRight each has the same value.
    The topRight have different values so we divide it into 4 sub-grids where each has the same value.
    Explanation is shown in the photo below:
    
![](https://assets.leetcode.com/uploads/2020/02/12/e2tree.png) 

**Constraints:**

*   `n == grid.length == grid[i].length`
*   <code>n == 2<sup>x</sup></code> where `0 <= x <= 6`

## Solution

```csharp
using System.Text;

public class Node {
    public bool val;
    public bool isLeaf;
    public Node? topLeft;
    public Node? topRight;
    public Node? bottomLeft;
    public Node? bottomRight;

    public Node(bool val, bool isLeaf) {
        this.val = val;
        this.isLeaf = isLeaf;
        this.topLeft = null;
        this.topRight = null;
        this.bottomLeft = null;
        this.bottomRight = null;
    }

    public Node(
        bool val,
        bool isLeaf,
        Node? topLeft,
        Node? topRight,
        Node? bottomLeft,
        Node? bottomRight) {
        this.val = val;
        this.isLeaf = isLeaf;
        this.topLeft = topLeft;
        this.topRight = topRight;
        this.bottomLeft = bottomLeft;
        this.bottomRight = bottomRight;
    }

    public override string ToString() {
        StringBuilder sb = new StringBuilder();
        sb.Append(GetNodeString(this));
        sb.Append(GetNodeString(topLeft));
        sb.Append(GetNodeString(topRight));
        sb.Append(GetNodeString(bottomLeft));
        sb.Append(GetNodeString(bottomRight));
        return sb.ToString();
    }

    private string GetNodeString(Node? node) {
        if (node == null) {
            return "[]";
        }
        return $"[{(node.isLeaf ? "1" : "0")},{(node.val ? "1" : "0")}]";
    }
}

/*
// Definition for a QuadTree node.
public class Node {
    public bool val;
    public bool isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;

    public Node() {
        val = false;
        isLeaf = false;
        topLeft = null;
        topRight = null;
        bottomLeft = null;
        bottomRight = null;
    }
    
    public Node(bool _val, bool _isLeaf) {
        val = _val;
        isLeaf = _isLeaf;
        topLeft = null;
        topRight = null;
        bottomLeft = null;
        bottomRight = null;
    }
    
    public Node(bool _val,bool _isLeaf,Node _topLeft,Node _topRight,Node _bottomLeft,Node _bottomRight) {
        val = _val;
        isLeaf = _isLeaf;
        topLeft = _topLeft;
        topRight = _topRight;
        bottomLeft = _bottomLeft;
        bottomRight = _bottomRight;
    }
}
*/
public class Solution {
    public Node Construct(int[][] grid) {
        return OptimizedDfs(grid, 0, 0, grid.Length);
    }

    private Node OptimizedDfs(int[][] grid, int rowStart, int colStart, int len) {
        int zeroCount = 0;
        int oneCount = 0;
        for (int row = rowStart; row < rowStart + len; row++) {
            bool isBreak = false;
            for (int col = colStart; col < colStart + len; col++) {
                if (grid[row][col] == 0) {
                    zeroCount++;
                } else {
                    oneCount++;
                }
                if (oneCount > 0 && zeroCount > 0) {
                    // We really no need to scan all.
                    // Once we know there are both 0 and 1 then we can break.
                    isBreak = true;
                    break;
                }
            }
            if (isBreak) {
                break;
            }
        }
        if (oneCount > 0 && zeroCount > 0) {
            int midLen = len / 2;
            Node topLeft = OptimizedDfs(grid, rowStart, colStart, midLen);
            Node topRight = OptimizedDfs(grid, rowStart, colStart + midLen, midLen);
            Node bottomLeft = OptimizedDfs(grid, rowStart + midLen, colStart, midLen);
            Node bottomRight = OptimizedDfs(grid, rowStart + midLen, colStart + midLen, midLen);
            bool isLeaf = false;
            return new Node(true, isLeaf, topLeft, topRight, bottomLeft, bottomRight);
        } else {
            bool resultVal = oneCount > 0;
            bool isLeaf = true;
            return new Node(resultVal, isLeaf);
        }
    }
}
```