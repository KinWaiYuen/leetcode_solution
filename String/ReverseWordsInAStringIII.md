# Reverse Words in a String III

@(算法)

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

**示例 1:**
```powershell
输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc"
```

## 方法：

思路也是很直接的，主要考虑的一个特殊例子是，**字符串的最后一个单词，不要忘记进行翻转了。**

```cpp
class Solution {
public:
    string reverseWords(string s) {
        int iStart = 0;
        int iEnd = 0;
        for (int i = 0; i <= s.length(); i++)
        {
            if (s[i] == ' ' || i == s.length())
            {
                // 翻转单词
                iEnd = i - 1;
                for (int j = iStart; j <= (iStart + iEnd) / 2; j++)
                {
                    auto temp = s[j];
                    s[j] = s[iStart + (iEnd - j)];
                    s[iStart + (iEnd - j)] = temp;
                }
                iStart = iEnd = i + 1;
            }
        }
        
        return s;
    }
};
```
