# Ambiguous Coordinates

@(算法)

我们有一些二维坐标，如 `"(1, 3)"` 或 `"(2, 0.5)"`，然后我们移除所有逗号，小数点和空格，得到一个字符串`S`。返回所有可能的原始字符串到一个列表中。

原始的坐标表示法不会存在多余的零，所以不会出现类似于"00", "0.0", "0.00", "1.0", "001", "00.01"或一些其他更小的数来表示坐标。此外，一个小数点前至少存在一个数，所以也不会出现“.1”形式的数字。

最后返回的列表可以是任意顺序的。而且注意返回的两个数字中间（逗号之后）都有一个空格。

```powershell
示例 1:
输入: "(123)"
输出: ["(1, 23)", "(12, 3)", "(1.2, 3)", "(1, 2.3)"]
```

```powershell
示例 2:
输入: "(00011)"
输出:  ["(0.001, 1)", "(0, 0.011)"]
解释: 
0.0, 00, 0001 或 00.01 是不被允许的。
```

```powershell
示例 3:
输入: "(0123)"
输出: ["(0, 123)", "(0, 12.3)", "(0, 1.23)", "(0.1, 23)", "(0.1, 2.3)", "(0.12, 3)"]
```

```powershell
示例 4:
输入: "(100)"
输出: [(10, 0)]
解释: 
1.0 是不被允许的。
```

**提示:**

+ `4 <= S.length <= 12`.
+ `S[0]` = "(", `S[S.length - 1]` = ")", 且字符串 `S` 中的其他元素都是数字。


## 方法：

只要区分好情况和判断规则即可，不算特别复杂。

```cpp
class Solution {
public:
    vector<string> ambiguousCoordinates(string s) {
        std::vector<std::string> result;
        for (int i = 1; i < s.length() - 2; i++)
        {
            std::string sFirst = s.substr(1, i);
            std::string sSecond = s.substr(1 + i, s.length() - 2 -i);
            std::vector<std::string> vecFirst = getNumber(sFirst);
            std::vector<std::string> vecSecond = getNumber(sSecond);
            
            for (int j = 0; j < vecFirst.size(); j++)
            {
                for (int k = 0; k < vecSecond.size(); k++)
                {
                    result.push_back("(" + vecFirst[j] + ", " + vecSecond[k] + ")");
                }
            }
        }
        
        return result;
    }
    
    std::vector<std::string> getNumber(std::string word)
    {
        std::vector<std::string> result;
        std::string sTmp;
        
        // 不加小数点的情况
        if (word.length() == 1 || (word.length() > 1 && word[0] != '0'))
        {
            result.push_back(word);
        }
        
        for (int i = 1; i < word.length(); i++)
        {
            sTmp = word.substr(0, i) + "." + word.substr(i);
            if ((sTmp[0] == '0' && sTmp[1] != '.') || (sTmp[sTmp.length() - 1] == '0'))
            {
                continue;
            }
            result.push_back(sTmp);
        }
        
        return result;
    }
};
```
