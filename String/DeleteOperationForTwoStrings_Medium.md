# *Delete Operation for Two Strings*

@(算法)

给定两个单词 word1 和 word2，找到使得 word1 和 word2 相同所需的最小步数，每步可以删除任意一个字符串中的一个字符。

**示例 1:**
```powershell
输入: "sea", "eat"
输出: 2
解释: 第一步将"sea"变为"ea"，第二步将"eat"变为"ea"
```

**说明:**
1. 给定单词的长度不超过500。
2. 给定单词中的字符只含有小写字母。


## 方法：动态规划，最长公共子序列（LCS）

这道题目想了好久，不会做，上网看了下答案，有这个最长公共子序列的东西，然后使用动态规划，题目要求的步数就是word1 + word2 - 2 * lcs。之前上大学有印象的看过这个东西，但是现在完全忘记了，只好后面慢慢积累。

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int length1 = word1.size();
        int length2 = word2.size();
        
        vector<vector<int> > dp(length1 + 1, vector<int>(length2 + 1, 0));
        
        for (int i = 1; i <= length1; i++)
        {
            for (int j = 1; j <= length2; j++)
            {
                if (word1[i - 1] == word2[j - 1])
                {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }
                else
                {
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        
        return length1 + length2 - 2 * dp[length1][length2];
    }
};
```
