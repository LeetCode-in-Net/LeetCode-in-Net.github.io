[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 210\. Course Schedule II

Medium

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you **must** take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.

*   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return _the ordering of courses you should take to finish all courses_. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

**Example 1:**

**Input:** numCourses = 2, prerequisites = \[\[1,0]]

**Output:** [0,1]

**Explanation:**

    There are a total of 2 courses to take. To take course 1 you should have finished course 0.
    So the correct course order is [0,1].

**Example 2:**

**Input:** numCourses = 4, prerequisites = \[\[1,0],[2,0],[3,1],[3,2]]

**Output:** [0,2,1,3]

**Explanation:**

    There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
    So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].

**Example 3:**

**Input:** numCourses = 1, prerequisites = []

**Output:** [0] 

**Constraints:**

*   `1 <= numCourses <= 2000`
*   `0 <= prerequisites.length <= numCourses * (numCourses - 1)`
*   `prerequisites[i].length == 2`
*   <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
*   <code>a<sub>i</sub> != b<sub>i</sub></code>
*   All the pairs <code>[a<sub>i</sub>, b<sub>i</sub>]</code> are **distinct**.

## Solution

```csharp
using System.Collections.Generic;

public class Solution {
    public int[] FindOrder(int numCourses, int[][] prerequisites) {
        var graph = new Dictionary<int, List<int>>();
        for (int i = 0; i < numCourses; i++) {
            graph[i] = new List<int>();
        }
        foreach (var classes in prerequisites) {
            graph[classes[0]].Add(classes[1]);
        }
        var output = new List<int>();
        var visited = new Dictionary<int, bool>();
        foreach (var c in graph.Keys) {
            if (Dfs(c, graph, visited, output)) {
                return new int[0];
            }
        }
        return output.ToArray();
    }

    private bool Dfs(int course, Dictionary<int, List<int>> graph, Dictionary<int, bool> visited, List<int> output) {
        if (visited.ContainsKey(course)) {
            return visited[course];
        }
        visited[course] = true;
        foreach (var c in graph[course]) {
            if (Dfs(c, graph, visited, output)) {
                return true;
            }
        }
        visited[course] = false;
        output.Add(course);
        return false;
    }
}
```