# Detect Capital

@(算法)

给定一个单词，你需要判断单词的大写使用是否正确。

我们定义，在以下情况时，单词的大写用法是正确的：

1. 全部字母都是大写，比如"USA"。
2. 单词中所有字母都不是大写，比如"leetcode"。
3. 如果单词不只含有一个字母，只有首字母大写， 比如 "Google"。

否则，我们定义这个单词没有正确使用大写字母。

**示例 1:**

```powershell
输入: "USA"
输出: True
```

**示例 2:**

```powershell
输入: "FlaG"
输出: False
```

**注意:** 输入是由大写和小写拉丁字母组成的非空单词。

## 方法：

没啥好说的。

```cpp
class Solution {
public:
    bool detectCapitalUse(string word) {
        if (word.length() > 1)
        {
            bool bCheckLower = false;
            if (word[0] >= 'a' && word[0] <= 'z')
            {
                bCheckLower = true;
            }
            else if ((word[0] >= 'A' && word[0] <= 'Z') && (word[1] >= 'a' && word[1] <= 'z'))
            {
                bCheckLower = true;
            }
            else
            {
                bCheckLower = false;
            }
            
            for (int i = 1; i < word.length(); i++)
            {
                if (bCheckLower && (word[i] >= 'A' && word[i] <= 'Z'))
                {
                    return false;
                }
                else if (!bCheckLower && (word[i] >= 'a' && word[i] <= 'z'))
                {
                    return false;
                }
            }
        }
        
        return true;
    }
};
```

