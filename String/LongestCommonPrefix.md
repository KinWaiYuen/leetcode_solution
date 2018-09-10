# Longest Common Prefix

@(算法)

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例 1:**
```powershell
输入: ["flower","flow","flight"]
输出: "fl"
```

**示例 2:**
```powershell
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

**说明:**

所有输入只包含小写字母 `a-z` 。


## 方法：

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        std::string sPrefix = "";
        std::string sTmp;
        bool bStop = false;
        
        if (strs.size() == 0) return "";
        if (strs.size() == 1) return strs[0];
        for (int i = 1; i <= strs[0].size(); i++)
        {
            sTmp = strs[0].substr(0, i);
            
            for (int j = 1; j < strs.size(); j++)
            {
                if (strs[j].find(sTmp) != 0)
                {
                    // 不符合前缀
                    bStop = true;
                    break;
                }
            }
            
            if (bStop)
            {
                break;
            }
            else
            {
                sPrefix = sTmp;
            }
        }
        
        return sPrefix;
    }
};
```
