# *Valid Palindrome II*

@(算法)

给定一个非空字符串 `s`，最多删除一个字符。判断是否能成为回文字符串。

**示例 1:**
```powershell
输入: "aba"
输出: True
```

**示例2：**
```powershell
输入: "abca"
输出: True
解释: 你可以删除c字符。
```

**注意:**

1. 字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。


## 方法：

使用头尾两个下标变量，遇到不相等的时候，不是选择马上返回`false`，而是尝试跳过，判断剩下的是否回文。

```cpp
class Solution {
public:
    bool validPalindrome(string s) {
        int i = 0;
        int j = s.length() - 1;
        
        while (i < j)
        {
            if (s[i] != s[j])
            {
                if (isPalindromeIgnoreIndex(s, i + 1, j))
                {
                    return true;
                }
                else if (isPalindromeIgnoreIndex(s, i, j - 1))
                {
                    return true;
                }
                else
                {
                    return false;
                }
            }
            i++;
            j--;
        }
        
        return true;
    }
    
    bool isPalindromeIgnoreIndex(std::string s, int start, int end)
    {
        while (start < end)
        {
            if (s[start] != s[end])
            {
                return false;
            }
            start++;
            end--;
        }
        
        return true;
    }
};
```

