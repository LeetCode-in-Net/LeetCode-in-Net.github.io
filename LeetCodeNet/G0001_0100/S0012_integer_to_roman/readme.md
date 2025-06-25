[![](https://img.shields.io/github/stars/LeetCode-in-Net/LeetCode-in-Net?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net)
[![](https://img.shields.io/github/forks/LeetCode-in-Net/LeetCode-in-Net?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Net/LeetCode-in-Net/fork)

## 12\. Integer to Roman

Medium

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

    Symbol   Value
     I        1
     V        5
     X        10
     L        50
     C        100
     D        500
     M        1000

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

*   `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
*   `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
*   `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral.

**Example 1:**

**Input:** num = 3

**Output:** "III" 

**Example 2:**

**Input:** num = 4

**Output:** "IV" 

**Example 3:**

**Input:** num = 9

**Output:** "IX" 

**Example 4:**

**Input:** num = 58

**Output:** "LVIII"

**Explanation:** L = 50, V = 5, III = 3. 

**Example 5:**

**Input:** num = 1994

**Output:** "MCMXCIV"

**Explanation:** M = 1000, CM = 900, XC = 90 and IV = 4. 

**Constraints:**

*   `1 <= num <= 3999`

## Solution

```csharp
public class Solution
{
    public string IntToRoman(int num)
    {
        var sb = new System.Text.StringBuilder();
        int m = 1000;
        int c = 100;
        int x = 10;
        int i = 1;
        num = Numerals(sb, num, m, ' ', ' ', 'M');
        num = Numerals(sb, num, c, 'M', 'D', 'C');
        num = Numerals(sb, num, x, 'C', 'L', 'X');
        Numerals(sb, num, i, 'X', 'V', 'I');
        return sb.ToString();
    }

    private int Numerals(System.Text.StringBuilder sb, int num, int one, char cTen, char cFive, char cOne)
    {
        int div = num / one;
        switch (div)
        {
            case 9:
                sb.Append(cOne);
                sb.Append(cTen);
                break;
            case 8:
                sb.Append(cFive);
                sb.Append(cOne);
                sb.Append(cOne);
                sb.Append(cOne);
                break;
            case 7:
                sb.Append(cFive);
                sb.Append(cOne);
                sb.Append(cOne);
                break;
            case 6:
                sb.Append(cFive);
                sb.Append(cOne);
                break;
            case 5:
                sb.Append(cFive);
                break;
            case 4:
                sb.Append(cOne);
                sb.Append(cFive);
                break;
            case 3:
                sb.Append(cOne);
                sb.Append(cOne);
                sb.Append(cOne);
                break;
            case 2:
                sb.Append(cOne);
                sb.Append(cOne);
                break;
            case 1:
                sb.Append(cOne);
                break;
            default:
                break;
        }
        return num - (div * one);
    }
}
```