# *Decode Ways*

@(算法)

一条包含字母 `A-Z` 的消息通过以下方式进行了编码：
```powershell
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

给定一个只包含数字的**非空**字符串，请计算解码方法的总数。

**示例 1:**
```powershell
输入: "12"
输出: 2
解释: 它可以解码为 "AB"（1 2）或者 "L"（12）。
```

**示例 2:**
```powershell
输入: "226"
输出: 3
解释: 它可以解码为 "BZ" (2 26), "VF" (22 6), 或者 "BBF" (2 2 6) 。
```

## 方法：动态规划

记录每一位的字符串，首先赋值：`dp[i] = dp[i - 1]`，然后我们再确定前两位到底能否组成一个26位字母，如果可以，再加上：`dp[i] += dp[i - 2];`。

```cpp
class Solution {
public:
    int numDecodings(string s) {
        if (s.empty() || (s.length() > 0 && s[0] == '0'))
        {
            return 0;
        }
        std::vector<int> dp(s.length() + 1, 0);
        dp[0] = 1;
        
        for (int i = 1; i < dp.size(); i++)
        {
            if (s[i - 1] == '0')
            {
                dp[i] = 0;
            }
            else
            {
                dp[i] = dp[i - 1];
            }
            
            if (i > 1 && (s[i - 2] == '1' || (s[i - 2] == '2' && s[i - 1] <= '6')) )
            {
                dp[i] += dp[i - 2];
            }
        }
        
        return dp[dp.size() - 1];
    }
};
```
