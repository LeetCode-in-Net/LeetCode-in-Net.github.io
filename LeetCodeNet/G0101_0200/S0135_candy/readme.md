[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 135\. Candy

Hard

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

*   Each child must have at least one candy.
*   Children with a higher rating get more candies than their neighbors.

Return _the minimum number of candies you need to have to distribute the candies to the children_.

**Example 1:**

**Input:** ratings = [1,0,2]

**Output:** 5

**Explanation:** You can allocate to the first, second and third child with 2, 1, 2 candies respectively. 

**Example 2:**

**Input:** ratings = [1,2,2]

**Output:** 4

**Explanation:** You can allocate to the first, second and third child with 1, 2, 1 candies respectively. The third child gets 1 candy because it satisfies the above two conditions. 

**Constraints:**

*   `n == ratings.length`
*   <code>1 <= n <= 2 * 10<sup>4</sup></code>
*   <code>0 <= ratings[i] <= 2 * 10<sup>4</sup></code>

## Solution

```csharp
using System;

public class Solution {
    private bool isFirstIteration;

    public enum RatingState {
        increase,
        decrease,
        stable,
        none
    }

    private RatingState GetNewState(int prevRating, int currentRating) {
        if (currentRating > prevRating) {
            return RatingState.increase;
        }
        if (currentRating < prevRating) {
            return RatingState.decrease;
        }
        return RatingState.stable;
    }

    private void CountSum(RatingState currentState, ref int n, ref int totalCandies, ref int startNum) {
        int res = 0;
        switch (currentState) {
            case (RatingState.increase):
                if (!isFirstIteration) {
                    startNum++;
                }
                res = (2 * startNum + n - 1) * (n) / 2;
                totalCandies += res;
                startNum = startNum + n - 1;
                break;
            case (RatingState.decrease):
                if (!isFirstIteration){
                    startNum--;
                }
                var start = startNum - n + 1;
                var end = startNum;
                res = (end + start) * n / 2;
                totalCandies += res;
                if (start <= 0) {
                    start--;
                    int toRemove = 0;
                    if (isFirstIteration)
                        toRemove = -1;
                    totalCandies += (n + 1 + toRemove) * (-start);
                }
                else if (start > 1) {
                    totalCandies -= (start - 1) * (n);
                }
                startNum = 1;
                break;
            case (RatingState.stable):
                totalCandies += n;
                startNum = 1;
                break;
            case (RatingState.none):
                return;
        }
        isFirstIteration = false;
        n = 1;
    }

    public int Candy(int[] ratings) {
        if (ratings.Length == 1) {
            return 1;
        }
        RatingState currentState = RatingState.none;
        int prevRating = ratings[0];
        int totalCandies = 0;
        int n = 2;
        int startNum = 1;
        isFirstIteration = true;
        for (int i = 1; i < ratings.Length; i++) {
            var newState = GetNewState(prevRating, ratings[i]);
            prevRating = ratings[i];
            if (newState != currentState) {
                CountSum(currentState, ref n, ref totalCandies, ref startNum);
                currentState = newState;
            } else {
                n++;
            }
        }
        CountSum(currentState, ref n, ref totalCandies, ref startNum);
        return totalCandies;
    }
}
```