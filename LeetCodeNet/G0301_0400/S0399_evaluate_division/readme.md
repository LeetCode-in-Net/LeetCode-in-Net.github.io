[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 399\. Evaluate Division

Medium

You are given an array of variable pairs `equations` and an array of real numbers `values`, where <code>equations[i] = [A<sub>i</sub>, B<sub>i</sub>]</code> and `values[i]` represent the equation <code>A<sub>i</sub> / B<sub>i</sub> = values[i]</code>. Each <code>A<sub>i</sub></code> or <code>B<sub>i</sub></code> is a string that represents a single variable.

You are also given some `queries`, where <code>queries[j] = [C<sub>j</sub>, D<sub>j</sub>]</code> represents the <code>j<sup>th</sup></code> query where you must find the answer for <code>C<sub>j</sub> / D<sub>j</sub> = ?</code>.

Return _the answers to all queries_. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

**Example 1:**

**Input:** equations = \[\["a","b"],["b","c"]], values = [2.0,3.0], queries = \[\["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]

**Output:** [6.00000,0.50000,-1.00000,1.00000,-1.00000]

**Explanation:**

Given: _a / b = 2.0_, _b / c = 3.0_

queries are: _a / c = ?_, _b / a = ?_, _a / e = ?_, _a / a = ?_, _x / x = ?_

return: [6.0, 0.5, -1.0, 1.0, -1.0 ]

**Example 2:**

**Input:** equations = \[\["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = \[\["a","c"],["c","b"],["bc","cd"],["cd","bc"]]

**Output:** [3.75000,0.40000,5.00000,0.20000]

**Example 3:**

**Input:** equations = \[\["a","b"]], values = [0.5], queries = \[\["a","b"],["b","a"],["a","c"],["x","y"]]

**Output:** [0.50000,2.00000,-1.00000,-1.00000]

**Constraints:**

*   `1 <= equations.length <= 20`
*   `equations[i].length == 2`
*   <code>1 <= A<sub>i</sub>.length, B<sub>i</sub>.length <= 5</code>
*   `values.length == equations.length`
*   `0.0 < values[i] <= 20.0`
*   `1 <= queries.length <= 20`
*   `queries[i].length == 2`
*   <code>1 <= C<sub>j</sub>.length, D<sub>j</sub>.length <= 5</code>
*   <code>A<sub>i</sub>, B<sub>i</sub>, C<sub>j</sub>, D<sub>j</sub></code> consist of lower case English letters and digits.

## Solution

```csharp
using System;
using System.Collections.Generic;

public class Solution {
    private Dictionary<string, string> root;
    private Dictionary<string, double> rate;

    public double[] CalcEquation(
            IList<IList<string>> equations, double[] values, IList<IList<string>> queries) {
        root = new Dictionary<string, string>();
        rate = new Dictionary<string, double>();
        int n = equations.Count;
        foreach (var equation in equations) {
            string x = equation[0];
            string y = equation[1];
            root[x] = x;
            root[y] = y;
            rate[x] = 1.0;
            rate[y] = 1.0;
        }
        for (int i = 0; i < n; ++i) {
            string x = equations[i][0];
            string y = equations[i][1];
            union(x, y, values[i]);
        }
        double[] result = new double[queries.Count];
        for (int i = 0; i < queries.Count; ++i) {
            string x = queries[i][0];
            string y = queries[i][1];
            if (!root.ContainsKey(x) || !root.ContainsKey(y)) {
                result[i] = -1;
                continue;
            }
            string rootX = findRoot(x, x, 1.0);
            string rootY = findRoot(y, y, 1.0);
            result[i] = rootX.Equals(rootY) ? rate[x] / rate[y] : -1.0; 
        }
        return result;
    }

    private void union(string x, string y, double v) {
        string rootX = findRoot(x, x, 1.0);
        string rootY = findRoot(y, y, 1.0);
        root[rootX] = rootY;
        double r1 = rate[x];
        double r2 = rate[y];
        rate[rootX] = v * r2 / r1;
    }

    private string findRoot(string originalX, string x, double r) {
        if (root[x].Equals(x)) {
            root[originalX] = x;
            rate[originalX] = r * rate[x];
            return x;
        }
        return findRoot(originalX, root[x], r * rate[x]);
    }
}
```